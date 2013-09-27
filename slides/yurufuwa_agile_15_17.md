# ゆるふわアジャイル
### アジャイルソフトウェア開発の奥義 読書会第XX回

@siguremon - 2013/09/28

---

## アジャイルの価値

- プロセスやツールよりも、人と人同士の交流を
- 包括的なドキュメントよりも、動作するソフトウェアを
- 契約上の交渉よりも、顧客との協調を
- 計画に従うよりも、変化に対応することを

---

## 今回のテーマ

- 第3部 給与システムのケーススタディ
  - 第15章 FacadeパターンとMediatorパターン
  - 第16章 Singletonパターンとmonostateパターン
  - 第17章 Null Objectパターン

---

## 第15章 FacadeパターンとMediatorパターン

-  方針を強制する
 - Facadeパターン 上から強制 
 - Mediatorパターン 下から強制

---

### 15.1 Facadeパターン


--

- 複雑で汎用的なインターフェースを持つオブジェクトの集団に、シンプルかつ共通のインターフェースを持たせたいときに使う
- 使用するクラスが詳細を必要がなくなる
- 使用するクラスにはシンプルで特化したインターフェースのみが見える
- 特化したインターフェースのみを使用するという方針を課す

--


- 例: java.sqlパッケージの機能にDBというラッパークラスをかぶせる
 - ApplicationクラスはDBクラスのみ知っていればよい
 - java.sqlの汎用的で複雑な部分が隠蔽される
 - データベースの呼び出しは全てDBクラスを通して行うという方針を課している 

--

#### メリット

- アプリケーション側のコードがシンプルになる
- アプリケーションと隠蔽された側が疎結合になる

--

#### デメリット

- 複雑なことをやろうとするとメソッドが増える（そのまま呼ぶのと変わらなくなる）


---

### 15.2 Mediatorパターン

--

- Mediator = 仲介者
- オブジェクト間のやりとりを仲介する
- 各オブジェクトは直接やりとりせず、Mediatorにメッセージを投げる
- メッセージを受け取ったMediatorが関連するオブジェクトにメッセージを投げる

--

- 例：テキストフィールドに文字を入力するとマッチしたリストアイテムがハイライトされる
 - テキストフィールド ->[入力イベント]-> Mediator
 - Mediator ->[ハイライト]->リストアイテム

--

#### メリット

- 各オブジェクトはお互いを知らなくてよい

--

#### デメリット
 - Mediatorが全てのオブジェクトを知っている必要がある
 - Mediatorはオブジェクトに強く依存するため、使い回せることがほぼない
 - 各オブジェクトはMediatorから呼ばれることを考慮する必要がある

---

## 第16章 Singletonパターンとmonostateパターン

オブジェクトが1つだけしか存在しないこと（唯一性・特異性）を保証するメカニズム

---

### 16.1 Singletonパターン

--

- コンストラクタをprivateに
- public staticなInstanceメソッドを通してインスタンスを生成・取得
 - 1回目の呼び出し: インスタンスを生成して返す
 - 2回目以降の呼び出し: 1回目で生成したインスタンスを返す

--

### Singletonの実装

```java:
public Class Singleton {
    private static Singleton theInstance = null;
	private Singleton() {}
	
	public static SingletonInstance() {
	    if (theInstance == null) {
		    theInstance = new Singleton();
		}
		return theInstance;
	}
}

```

--

### 16.1.1 メリット

- クロスプラットフォーム
- あらゆるクラスで利用可能
- 派生を使って生成することが可能
- 評価が簡単

--

### 16.1.2 デメリット

- オブジェクトの破壊が定義されていない
- 継承できない
- 効率性

--

### 16.1.3 Singletonの利用例

- 本文参照

---

### 16.2 Monostateパターン

--

- 同じクラスの異なるインスタンスがあたかも1つのように振る舞う
- メソッドは全てstaticでない

--

```java:
public class Monostate {
    private static int itsX = 0;

    public Monostate() {}
	
	public void setX(int x) {
	    itsX = x;
	}
	
	public int getX() {
        return itsX;
	}
}
```

--


### 16.2.1 メリット

- わかりやすさ
- 派生可能
- 多態性（ポリモーフィズム）
 - メソッドがstaticでないのでオーバーライド可能
- 生成と破壊の定義が明確

--

### 16.2.2 デメリット

- 変換不能
- 効率性
- 存在
- プラットフォームに依存

--

### 16.2.3 Monostateの利用例

- 本文参照

---

## 第17章 Null Objectパターン

--

- Null Objectを使わない場合

```java:
Employee e = DB.getEmployee("Bob");
if ( e != null && e.isTimeToPay(today))
    e.pay();
```

--

### Null Objectを使った場合

```java:
Employee e = DB.getEmployee("Bob");
if (e.isTimeToPay(today))
    e.pay();
```

--

### Null Objectの実装例

```java:
public interface Employee {
    public boolean isTimePay(Date payDate);
	public void pay();
	public static final Employee NULL = new Employee() {
	   public boolean isTimeToPay(Date payDate) {
	       return false;
	   }
	   
	   public void pay() {
	   }
	};
}
```

---

## まとめ

--

### FacadeパターンとMediatorパターン
 - 方針をオブジェクトに強制する
 - 明示的な強制=Facade
 - 悲鳴時的な強制=Mediator

--

### SingletonパターンとMonostateパターン
 - オブジェクトの唯一性を保証する
 - インスタンスを1つしか作らせない=Singleton
 - static変数により1つであるかのように振る舞う=Monostate

--

###  Null Objectパターン
 - nullの代わりにnullを意味するオブジェクトを定義
 - nullチェックを不要にする
