# TIL-Today-I-Learned- 20200618(Thur)


## [React iterative(map)](https://www.youtube.com/watch?v=OO5gXdPR6HI&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=22)

- To write 5 "like"s, html needs to write 5 <li> codes

  ```html
  <ul>
  	<li>like</li>
      <li>like</li>
      <li>like</li>
      <li>like</li>
      <li>like</li>
  </ul
  ```

- However, this can be simplified using map() function

  ```react
  <ul>
      {['like', 'like', 'like', 'like', 'like']}.map(() => {
          return (
              <li>like</li>
          );
      })
  </ul>
  
  <ul>
      {['사과', '바나나', '포도', '귤', '감', '배', '밤']}.map((v) => {
          return (
              <li>{v}</li>
          );
      })
  </ul>
  
  <ul>
      {['like']}.map((v) => {
          return (
              <li>{v}</li>
          );
      })
  </ul>
  ```



## [React iteration (key)](https://www.youtube.com/watch?v=A-ydulnj8lk&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=23)

- Two dimensional array

```react
<ul>
	{[
		['apple', 'sweet'],
		['banana', 'sweet'],
		['grape', 'sour'],
		['mandarin', 'sour'],
		['kiwi', 'sour'],
		['pear', 'sour'],
		['peach', 'sour'],
	]}.map((v) => {
		return (
			<li><b>{v[0]}</b> - {v[1]}</li>
		);
	}]
</ul>
```

- Object (more common)

```react
<ul>
	{[
		{ fruit: 'apple', taste: 'sweet'},
		{ fruit: 'banana', taste: 'sweet'},
		{ fruit: 'grape', taste: 'sour'},
		{ fruit: 'mandarin', taste: 'sour'},
		{ fruit: 'kiwi', taste: 'sour'},
		{ fruit: 'pear', taste: 'sour'},
		{ fruit: 'peach', taste: 'sour'},
	]}.map((v) => {
		return (
			<li><b>{v.fruit}</b> - {v.taste}</li>
		);
	}]
</ul>
```

- Props is used to solve object's lack of readability
  - Better performance
  - Need to add `key` and this should contain a unique value
  - `v.fruit` is not unique because there are two '사과's, but writing `v.fruit + v.tatse` is because the tastes are different.

```react
<ul>
	{[
		{ fruit: 'apple', taste: 'sweet'},
		{ fruit: 'banana', taste: 'sweet'},
		{ fruit: 'grape', taste: 'sour'},
		{ fruit: 'mandarin', taste: 'sour'},
		{ fruit: 'kiwi', taste: 'sour'},
		{ fruit: 'pear', taste: 'sour'},
		{ fruit: 'apple', taste: 'sour'},
	]}.map((v) => {
		return (
			<li key={v.fruit + v.tatse}><b>{v.fruit}</b> - {v.taste}</li>
		);
	})}
</ul>
```


- Index can be used as a parameter. But `i` should not be in the `key` if want to add `delete` element feature. (If elements are only added in the array, then `i` can be in the `key`)

  - The code below will print object's index in the place of `i`

    **apple** - 0

    **banana** - 1

    **grape** - 2

    .

    .

    .

```
<ul>
	{[
		{ fruit: 'apple', taste: 'sweet'},
		{ fruit: 'banana', taste: 'sweet'},
		{ fruit: 'grape', taste: 'sour'},
		{ fruit: 'mandarin', taste: 'sour'},
		{ fruit: 'kiwi', taste: 'sour'},
		{ fruit: 'pear', taste: 'sour'},
		{ fruit: 'apple', taste: 'sour'},
	]}.map((v, i) => {
		return (
			<li key={v.fruit + v.tatse}><b>{v.fruit}</b> - {i}</li>
		);
	})}
</ul>
```



- Several ways to write a function

  - Without return

    ```react
    <ul>
    {[
        
    ]}.map((v) => (
    	<li key={v.fruit + v.tatse}><b>{v.fruit}</b> - {v.taste}</li>
    	))}
    </ul>
    ```

  - Without paranthesis

    ```react
    <ul>
    {[
        
    ]}.map((v) => 
    	<li key={v.fruit + v.tatse}><b>{v.fruit}</b> - {v.taste}</li>
    	)}
    </ul>
    ```

    

## [Separating Components & Props](https://www.youtube.com/watch?v=6YZhSvRqddw&list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn&index=24)

- Array to be mapped can be stated separately

  ```
  fruits = [
		{ fruit: 'apple', taste: 'sweet'},
		{ fruit: 'banana', taste: 'sweet'},
		{ fruit: 'grape', taste: 'sour'},
		{ fruit: 'mandarin', taste: 'sour'},
		{ fruit: 'kiwi', taste: 'sour'},
		{ fruit: 'pear', taste: 'sour'},
		{ fruit: 'apple', taste: 'sour'},
  ];
  
  <ul>
  	{this.fruits.map((v, i) => {
  		return (
  			<li key={v.fruit + v.tatse}><b>{v.fruit}</b> - {i}</li>
  		);
  	})}
  </ul>
  ```

  

- The returned list can be separated to another file. This improves performance

  - Make a jsx file: "Try.jsx"

    ```react
    import React, { Component } from 'react';
    
    class Try extends Component{
    	render() {
    		return (
                <li>
                <b>{v.fruit}</b> - {i}
                <div>content1</div>
                <div>content2</div>
                <div>content3</div>
                </li>
            )
    	}
    }
    
    export default Try;
    ```

    

  - Import Try component. This can also be imported to other files.

  - However, just importing Try does not give any information on `v` and `i` in Try.jsx.  `props` is used to pass parameters to the Try component

  - `props` is called `attributes` in html

    ```react
    import Try from './Try'; // on top
    
    <ul>
    	{this.fruits.map((v, i) => {
    		return (
    			<Try value={v} index={i}/> //props
    		);
    	})}
    </ul>
    ```

    

  
