# Qcom.io
<!-- [![Dependency Status](https://david-dm.org/maheshkareeya/qcom.svg)](https://david-dm.org/maheshkareeya/qcom)
[![devDependency Status](https://david-dm.org/maheshkareeya/cli/dev-status.svg)](https://david-dm.org/maheshkareeya/cli#info=devDependencies) -->

<!-- [![Build Status](https://travis-ci.org/@qcom.io/qcom.svg?branch=master)](https://travis-ci.org/@qcom.io/qcom) -->
<!-- [![Coverage Status](https://coveralls.io/repos/github/maheshkareeya/qcom/badge.svg?branch=master)](https://coveralls.io/github/maheshkareeya/qcom?branch=master) -->

[![NPM version](https://badge.fury.io/js/%40qcom.io%2Fqcom.svg)](https://www.npmjs.com/package/@qcom.io/qcom)
![Downloads](https://img.shields.io/npm/dm/%40qcom.io%2Fqcom.svg?style=flat)

![demoofqcom](https://unpkg.com/@qcom.io/qcom@1.0.36/qcom.png)
### Javascript Framework

#### Installation

```bash
npm install @qcom.io/qcom
```
#### Or CLI Installation for Quick Start
```bash
npx @qcom.io/qcom-cli
npm start
```
### check url
http://localhost:8080

#### Or Use following code to your html file

```html
<script type="module">
  import $ from 'https://unpkg.com/@qcom.io/qcom'
  // Or import $ from './node_modules/@qcom.io/qcom/index.js'
  $() // Now check your Inspector of Browser He will guide you for further steps
</script>
```
#### index.html
```html
<qcom-hello-world></qcom-hello-world>

<script type="module">
  import $ from 'https://unpkg.com/@qcom.io/qcom'
  // Or import $ from './node_modules/@qcom.io/qcom/index.js'
  $({
      name:'QcomHelloWorld',
      template:()=>h1('Hello World')
  })
</script>
```

## Rules 
`HTML`
```html 
<h1 class="head"  style = "color:red;  background-color:  yellow"    id="heading" > I am H1 </h1>
```
`Qcom`
```js
h1({class:'head', style:{ color:'red', backgroundColor : 'Yellow' }, id:'heading' }, 'I am H1' )
```

#### Functions
```html
<qcom-functions></qcom-functions>

<script type="module">
  import $ from 'https://unpkg.com/@qcom.io/qcom'
  $({
      name:'QcomFunctions',
      template:()=>div(h1({click:'QcomFunctions.log()'},'Click Here')),
      code:{
          log:()=>{
              //Do something here
              alert('clicked')
          }
          //Create your own functions here like log()
      }
  })
</script>
```


#### Data Management
```html
<qcom-data></qcom-data>

<script type="module">
  import $ from 'https://unpkg.com/@qcom.io/qcom'
  $({
      name:'QcomData',
      data:{
          counter:0
      },
      template:()=>div( /* div must be here to wrap all internal tags*/
                        h1(this.data.counter),
                        button({click:'QcomData.add()'},'+'),
                        button({click:'QcomData.sub()'},'-')
                     ),
      code:{
            add:()=>{
                    this.data.counter +=  1
                    this.render()
            },
            sub:()=>{
                    this.data.counter -=  1
                    this.render()
            }
      }
  })
</script>
```

#### Loop
```html
<qcom-loop></qcom-loop>

<script type="module">
  import $ from 'https://unpkg.com/@qcom.io/qcom'
  $({
      name:'QcomLoop',
      data:{
          items:[{id:1,name:'Abigail',age:21},
                {id:2,name:'max',age:29},
                {id:3,name:'Alison',age:17},
                {id:4,name:'bob',age:32},
                {id:5,name:'brad',age:36}]
      },
      template:()=>div(
                    table(
                        tr(
                            td('Index'),
                            td('Name'),
                            td('Age')
                        ),
            ()=>this.data.items.map(item =>
                    tr(
                        td(item.id),
                        td(item.name),
                        td(item.age))
                        )
                    )
                )
  })
</script>
```

#### Get Api
```html
<qcom-get></qcom-get>

<script type="module">
import $ from 'https://unpkg.com/@qcom.io/qcom'
$({
    name:'QcomGet',
    data:{
        items:[]
    },
    template:()=>div(
        table(
            tr(
                td('Id'),
                td('Title'),
                td('completed')
            ),
            ()=>this.data.items.map(item =>
                    tr(
                        td(item.id),
                        td(item.title),
                        td(item.completed))
                        )
        )
    ),
    code:{
        onload:async ()=>{
            this.data.items = await qcom.get('https://jsonplaceholder.typicode.com/todos/')
            this.render()
        }
    }
})

</script>
```

#### Styling (camelCase is required while using style)
```html
<qcom-css-example></qcom-css-example>

<script type="module">
  import $,{color} from 'https://unpkg.com/@qcom.io/qcom'
  $({
      name:'QcomCssExample',
      globalcss:{ /* Global CSS*/
          '*':{
              margin:'50px',
              padding:'50px'
          }
      },
      css:{ /* Internal CSS*/
          h1:{
              color:color.red,
              cursor:'pointer',
              backgroundColor:color.yellow
          },
          '.mt':{
              marginTop:'5px'
          }
      },
      template:()=>div(
                        h1({class:'mt',style:{ /* Inline CSS*/
                            border:'2px solid red'
                        }},'Inline Internal and global Style')
                    )
  })

</script>
```
#### Qcom Router
```html
<qcom-main></qcom-main>
<script type="module">
import $ from 'https://unpkg.com/@qcom.io/qcom'
    let QcomOne = {
        name:'QcomOne',
        data:{
            items:[
                {name:'mahesh'},{name:'dipak'}
            ]
        },
        template:()=>div(h1('Page One'),
                ()=>this.data.items.map(item =>
                        div(item.name)))
    }
    let QcomTwo ={
        name:'QcomTwo',
        data:{
            items:[]
        },
        template:()=>row(
            col(form(
                material(
                    h1('Registration'),
                    input({id:'name',class:'mb6',placeholder:'Name'}),
                    input({id:'email',class:'mb6',placeholder:'Email'}),
                    input({id:'password',class:'mb6',placeholder:'Password'}),
                    right(btn({click:'QcomTwo.post()',is:'md'},'Submit')))
            )),
            col(table(
                tr(
                    td('Name'),
                    td('Email'),
                    td('Password')
                ),
                ()=>this.data.items.map(item =>
                        tr(td(item.name),
                            td(item.email),
                            td(item.password)))
            ))
        ),
        code:{
            post:()=>{
                this.data.items.push({
                    name:getval('name'),
                    email:getval('email'),
                    password:getval('password')
                })
                this.render()
            }
        }
    }
    let QcomError = {
        name:'QcomError',template:()=>div(
            h1('404 Page')
        )
    }
    $({
        name:'QcomMain',
        template:()=>div(
                appbar(
                    btn({route:'/QcomOne',is:'link', class:'ml12'},'One'),
                    btn({route:'/QcomTwo',is:'link', class:'ml12'},'Two'),
                    btn({route:'/QcomError',is:'link', class:'ml12'},'404')
                ),
                div({class:'mt12', id:'root'})
            ),
       include:[QcomOne,QcomTwo,QcomError],
            router:{
                root:'QcomOne',
                view:'root',
                error:$('QcomError')(),
                links:['QcomOne','QcomTwo']
            }
    })
</script>

```

### Demo
![demoofqcom](https://unpkg.com/@qcom.io/qcom@1.0.36/result.png)



**Grammar:**

```
                                        function
 ┌─────────-───────────────────────────────┴────────────────────────────────────────────────────────┐
 │                            separators                                                            |
 │                   ┌────────────┴───┬────────────────┬───────────────────────────┐                |
 |                   ↓                ↓                ↓                           ↓                |
p(  { to:'firstname' ,   class:'mt12' , id:'firstname' , style: {color:color.red} }, 'Hello World'  )
        └───┬───┘          └───┬───┘     └────┬───┘       └────┬────────┘                 |
            ┴───────────┬──────┴─────-──-─────┘-──-─────-─────-┘                          |
                   attributes                                                           Text
```

## Configuration


<details>
<summary>Use <code>color</code> : For color coding </summary>
<pre><code>
import $,{color} from 'https://unpkg.com/@qcom.io/qcom'
$({
    theme:{
        color:color.red,
        background:color.yellow
    }
})
</code></pre>
</details>
<br>
<details>
<summary>Use <code>to</code> : For Two way data binding</summary>
<pre><code>
        input({to:'email'}),
            p({to:'email'},'')
</code></pre>
</details>
<br>
<details>
<summary>Use <code>router</code> : For static and dynamic routing</summary>
<pre><code>
    template:()=>div(
            appbar(
                btn({route:'/QcomOne',is:'link', class:'ml12'},'One'),
                btn({route:'/QcomTwo',is:'link', class:'ml12'},'Two'),
            ),
            div({class:'mt12', id:'root'})    //<-|
        ),                                   //   |
        include:[QcomOne,QcomTwo,QcomError],//    |
        router:{                           //     |
            root:'QcomOne',               //      |
            view:'root', // id of div <-----------|
            error:$('QcomError')(),
            links:['QcomOne','QcomTwo']
        }
</code></pre>
</details>



### Colors 
![color00](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color00.png)
![color0](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color0.png)
![color1](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color1.png)
![color2](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color2.png)
![color3](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color3.png)
![color4](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color4.png)
![color5](https://unpkg.com/@qcom.io/qcom@1.0.36/raw/color5.png)



## License

[MIT](LICENSE)
