# Clean Code Principles

## 1. Meaningful Names

### Bad Code

```javascript
let d; // elapsed time in days
let x1; // initial position
```
### Good Code
```javascript
let elapsedTimeInDays;
let initialPosition;
```

# 2. Function Should Do One Thing

```javascript
function handleUserData(user){

    //Validate user
    if(!user.name || !user.email){
        console.log('Invalid user);
        return;
    }

    //save to database
    db.save(user);

    //send welcome email
    emailService.sendWelcomeEmai(user.email);
}
```


```javascript
function handleUserData(user){
    if(!isValidUser(user)) return;

    saveUserToDatabase(user);
    sendWelcomeEmail(user);
}

function isValidUser(user){
    return user.name && user.email;
}

function saveUserToDatabase(user){
    db.save(user);
}

function sendWelcomeEmail(user){
    emailService.sendWelcomeEmail(user.email)
}
```

# Avoid deep nesting

```javascript
function calculateDiscount(customer, products){

    if(customer.isPremium)  {
        if(products.length > 5) return 0.2;

        else {
            if(customer.years> 3) return 0.15;
            else return 0.1;
        }
    } else return 0; 
} 
```

```javascript
function calculateDiscount(customer, products){
     if(! customer.isPremium) return 0;

     if(products.length >5) return 0.2

     if(customer.years >3) return 0.15
}
```

# 4. User default parameters instead of conditionals

```javascript
function createrUser( name, role){
    const userRole = role || 'user';
    //...
}
```


```javascript
function createUser(name, role = 'user'){
    //...
}
```

# 5. Prefer Pure Functions


```javascript
let taxRate = 0.1;
function calculateTotal(price){
    return price+ (price*taxRate);   //depends on external state
}
```

```javascript
function calculateTax(price, taxRate= 0.1){
    return price + (price* taxRate);  //pure function
}
```




