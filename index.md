## AngularJSで作ったアプリをReactで置き換えてみた

---

## React

--

### React

- XML likeな構文(JSX)でComponentを定義
 - Componentを組み合わせてViewを構築
- 子Componentへの値の受け渡しにはPropsを使う
- ユーザーの操作などで変化する値にはStateを使う
- Componentの各状態においてLifecycle Methodが定義されてるのでよしなに使う

--

### Reactを使うにあたって

1.  Componentを洗い出す
2.  staticに作ってみる
3.  Stateを使うべきところを洗い出す
4.  Stateを置くところを決める
5.  子から親へデータを戻す

http://facebook.github.io/react/docs/thinking-in-react.html

---

## Component

--

### Component

- 実際に組み始める前にComponentの設計をする
 - 折角なのでBEMで考えてみる

```css
.members                         ->  <Members />
.members__list              ->  <MembersList />
.members__list__row  ->  <MembersListRow />
.member-edit                  ->  <MemberEdit />
```

--

### Component

- JSXでXMLのattributeのように書くことでComponentへPropsを渡すことができる
 - BEMのclassNameをPropsを使って渡してみる

```ruby
# <Members className="members" />

Members = React.createClass
  render: ->
    bemClassName =
      list: "#{@props.className}__list"
    <MembersList className={bemClassName.list} />
```

---

## State

--

### State

- `getInitialState`でstateを初期化
- `setState`でstateの値を変更
- `componentDidMount`でAPIリクエストをしてsetStateで更新するといいらしい
- 子Componentでstateの内容が変更されたら、イベントで親まで戻してあげる

```ruby
MembersList = React.createClass
  getInitialState:
    member: null
  componentDidMount: ->
    Api.members.get().done (member) =>
      @setState member: member
  handleMemberEdit: (member) ->
    @setState member: member
  render: ->
    <MembersListRow
      member={@state.member}
      onMemberEdit={@handleMemberEdit} />

MembersListRow = React.createClass
  handleSave: ->
    @props.onMemberEdit(member)
  render: ->
    <MemberEdit
      member={@props.member}
      onSave={@handleSave} />
```

--

### State

- 基本的にはStateは多用せずにPropsを使う
 - 親からpropsで与えられてたら、stateじゃない
 - 変化するものじゃなかったら、stateじゃない
 - 他のstateやpropsから処理されるものだったら、stateじゃない

http://facebook.github.io/react/docs/thinking-in-react.html#step-3-identify-the-minimal-but-complete-representation-of-ui-state

---

## AngularJS vs React

--

### DOM Component

- ReactのComponentの方が分割しやすい
 - 責任範囲を小さくできるのでコードが煩雑化しにくそう
 - 大きなComponentも作ろうと思えば作れるので設計大事
- className(Props)の引き回しでBEMが快適になる
 - `class=""`に頑張って書かなくていいのは嬉しい
 - やり過ぎると大変なことになりそうなのでほどほどに

--

### State change

- ngScopeが優秀
 - React.addonsの`Reactlink`を使うとtwo-way bindingできるらしい
- Componentのネストが深くなるとイベントで戻すのが辛くなる
- React.addonsの`classSet`を使うとAngular likeにclassNameの切り替えができる

---

## まとめ

--

### まとめ(感想)
- AngularJSやBackbone(Marionette)と比べるとViewのコンポーネント化がしやすい
 - BEMを始めCSSの設計手法との相性も良さそうな印象
- State周りは`Reactlink`を使うのが正解な気がする
- 他にもngAnimate風にアニメーションの指定ができるMixinがあったり面白そう
- JSXの取っ付きづらさに慣れると使いやすい

https://github.com/cancer/react-SavageApp

---

### ご清聴ありがとうございました

