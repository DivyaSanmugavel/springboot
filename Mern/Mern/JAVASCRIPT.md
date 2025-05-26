

Arrays and object Reference type:

```
const arr=['hello','hi'];

arr.push('gm');
 const ar=arr
 ar.push('hey')-->should not do like this for copy
 //instead
 const ar=arr.slice() 
 ar.push('hey') should not affect the original one
console.log(arr);

const ob={name:'kuna',age:23};
ob.name='mano';

console.log(ob)
```

HERE const rule did not change by updating the arrays stored in memory where the actual datas stored so there the data reallocating the size alone getting changed  

Can change the object values because of the reference 

---

SPREAD OPERATOR

```
const arr=['hello','hi'];

arr.push('gm');

const ar=[...arr];

ar.push('jj');

console.log(ar);

using object 
const ob={name:'kuna'};
ob.name='mano';
console.log(ob)
const ss={...ob,age:29};
console.log('final one',ss)
```

Copy the array to new array or object to fetch data from that syntax use spread operator

---
REST oprator->used inside the parameter before the paramter use ... 
```
const fun=(...args)=>{

    return args

}

console.log(fun(1,2,3,4,5,6))
```

### DESTRUCTURING:

**Destructuring** means:

> "Take values out of an object or array and put them into variables."

It helps you avoid writing repeated code.


```
//object:
const des={name:'john',age:20}

const {name,age}=des;

console.log(n,a)
//Arrays:

const rr=[1,2,3]

const [o,t,th]=rr;

console.log(o,t,th)

// Renaming in des:
let person = {
  name: "Bob",
  age: 30
};

let { name: myName } = person;
console.log(myName); // Bob


```

#### **SETTIMEOUT**

```
setTimeout(()=>{
        console.log("time done");
},3);
```
- schedules a function to be executed after ~3 milliseconds.

#### **CALLBACK FUNCTION**

```
const fetchData=(callback)=>{
    callback('fun');
}

setTimeout(()=>{

    fetchData((result)=>{

        console.log("time done",result);

    })

},3);
```

const fetchData=(callback)=>{
    callback();
}

Nothing runs here. JavaScript just **stores** it in memory. It says:

> "Okay, now I know what `fetchData` means. If someone calls it, I’ll know what to do.
> AFTER timeout
> 
`fetchData` is **called**.

fetchData(() => {
    console.log("time done");
});
You are **calling `fetchData()`**, and you're **passing a function as an argument**.  
This is called an **anonymous arrow function**. 
It's just like doing:

```
function tempFunc() {
    console.log("time done");
}
fetchData(tempFunc);

```
But instead of creating a separate function with a name, you're writing it **inline**. in above code

Now go inside `fetchData`

```
const fetchData = (callback) => {
    callback(); // 👈 This is calling the function you passed
};

```
So now:

- `callback` holds: `() => { console.log("time done"); }`
    
- So when you do `callback();`, it's the same as running:

```
() => {
  console.log("time done");
}();

output: time done
```

---
#### **PROMISE**

```
let mypromse=new Promise((myresolve,myreject)=>{
    setTimeout(()=>{

myresolve('data');
// myreject()

    },2000)
})
mypromse.then((data)=>{
    // console.log('resolv',data);
    return data
}).then((data)=>{
    console.log(data);
})
.catch(()=>{
console.log('reject');
})
```

### What is a `Promise`?

A **Promise** is a special JavaScript object that represents:

> "A task that will finish **later** (asynchronously-not at the same time or speed), and either:

- **succeed** (resolve) or
    
- **fail** (reject)"
- "I promise to give you data later (after some time), or I will reject it if something goes wrong."
## Where is this used in real life?

- **API requests** (fetch, axios)
    
- **Database calls**
    
- **File uploads**
    
- **Any async operation**

```
(resolve, reject) => { ... }

```
 Whenever you create a promise, the function inside the constructor **must accept two parameters**:

These functions are used to change the promise’s status:

- from **"pending"**
    
- to **"fulfilled"** (by calling `resolve(...)`)
    
- or **"rejected"** (by calling `reject(...)`)

- The **first parameter** → for success
    
- The **second parameter** → for failure

#### THEN

When the **data is available** (for example, from an API endpoint or after a delay), the Promise is **resolved**, and then `.then(...)` runs.

```
            🔄 Promise created
                   ↓
         ✅ Server responds with data
                   ↓
        ✔️ Promise is resolved (success)
                   ↓
            .then(...) runs

```

#### CATCH

```
            🔄 Promise created
                   ↓
       ❌ Server fails / no data
                   ↓
        ❌ Promise is rejected (error)
                   ↓
            .catch(...) runs

```

**What does "Promise is resolved" mean?**

> It means **"The task is finished successfully, and data is available now."**


### Real-world meaning:

Imagine you ordered food online (like Swiggy or Zomato):

- 📦 You place an order → this is like **creating a Promise**.
    
- 🕐 You're waiting → the Promise is **pending**.
    
- ✅ Food arrives → the Promise is **resolved** (success).
    
- ❌ Delivery failed → the Promise is **rejected** (failure).