### Screen Design
Screen No | Design
------------ | -------------
01 | [Enter Mobno](https://raw.githubusercontent.com/abbastec/agro/master/01EnterMobno.JPG)
02 | [OTP With Password](https://raw.githubusercontent.com/abbastec/agro/master/02OTPwithPassword.JPG)
03 | [Password Only Screen](https://raw.githubusercontent.com/abbastec/agro/master/03PasswordOnlyScreen.JPG)
04 | [Admin Home](https://raw.githubusercontent.com/abbastec/agro/master/04AdminHome.JPG)
05 | [Admin Payment](https://raw.githubusercontent.com/abbastec/agro/master/05AdminPayment.JPG)
06 | [Referral Code](https://raw.githubusercontent.com/abbastec/agro/master/06ReferalCode.JPG)
07 | [Home Screen Payment](https://raw.githubusercontent.com/abbastec/agro/master/07HomeScreenPayment.JPG)
08 | [Home Screen Matrix](https://raw.githubusercontent.com/abbastec/agro/master/08HomeScreenMatrix.JPG)

### API End Point

#### API 01: Mobile Number Login

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/01EnterMobno.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/01EnterMobno.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/mobno

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "9798977767"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] If Mobile Number exist in Database and [Status=2 or Status=3]
* - [ ] Return response status as 1. We can Navigate the screen to get password.
- [ ] If Mobile Number exist in Database and [Status=1]
* - [ ] Return response status will be 2. We can Navigate the screen to get OTP. 
* - [ ] Also API will send Generated OTP to respective mobile number. 
- [ ] If Mobile Number does not exist in Database we will throw 401 error 

### Sub Task (Secondary)
- [ ] Mobile Number Validation [10 numbers]
- [ ] Maximum OTP request for a mobile number is 3 [configurable] per day

------

#### API 02: Validate OTP and Set New Password

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/02OTPwithPassword.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/02OTPwithPassword.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/otp

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "979107099",
    "password": "Welcome123",
    "otp": "123456"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] Mobile Number should exist in database and [status in 1,2,3]
- [ ] OTP Validation
- [ ] Store the password in db as password_hash and password_salt

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation

------

#### API 03: Login with Password

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/03PasswordOnlyScreen.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/03PasswordOnlyScreen.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/auth

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "9791079311",
    "password": "Welcome123",
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```

:Token:
```javascript
{
  "mobile": "9791070319",
  "iat": 1593658604,
  "exp": 1593676604,
  "role": "user"
}
```

### Sub Task (Primary)
- [ ] Mobile Number should exist in database and [status in 2,3]
- [ ] Check for Password Validity with hashed db password
- [ ] Return JWT Token with payload { mobno: 9791070990, role: user or admin or  }
- [ ] If invalid Mobile number or password then return Error Code 401: Invalid Login details

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API 04: Admin: Get User Count

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/04AdminHome.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/04AdminHome.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
GET | http://localhost/agro/api/admin/usercount

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "count": "34054"
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Analysis needed. For test purpose we can make a entry in payment table

### Sub Task (Secondary)
- [ ] N/A

------

#### API 05: Admin: View Payment

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/05AdminPayment.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/05AdminPayment.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/admin/payment

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "view": "Last 5 days",
    "from_date": "",
    "to_date": ""
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
    "list": [
        { "user_name": "User Name", "mobno": "9791070888", "amt": "5000" },
        { "user_name": "User Name", "mobno": "9791070881", "amt": "5000" }
    ]
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] View, From Date and To Date are optional

### Sub Task (Secondary)
- [ ] Date Validation
- [ ] Future: Pull to refresh pagination may required.

------

#### API 06: User: Referral Registration

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/06ReferalCode.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/06ReferalCode.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
POST | http://localhost/agro/api/user/referralreg

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "first_name": "Senthil", 
    "last_name": "Perumal",
    "email": "senthil@gmail.com",
    "mobno": "9791078777",
    "referal_code": "37857uefj83u58utfio340895ui930it",
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok"
}
```
### Sub Task (Primary)
- [ ] Mobile Number should not exist in database and [status not in 1,2,3]
- [ ] Referal code should be valid and available for registration

### Sub Task (Secondary)
- [ ] First name, last name validation. Max Length: 50
- [ ] EMail Id Validation
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation [Min Length 8] [Characters Allowed: A-Z a-z 0-0 _ -] [Must have one alphabet and one number]
- [ ] Validate Referal Code

------

#### API 08: User: Get User Details [Name, Wallet, Matrix details]

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/08HomeScreenMatrix.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/08HomeScreenMatrix.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
GET | http://localhost/agro/api/user/details

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "wallet": "500",
    "matrix": {
        "usera": { id: "user id", "ref_code": "..code..", "status": "1", "name": "user_name", "mobno": "9791077718" },
        "userb": { id: "user id", "ref_code": "..code..", "status": "2", "name": "user_name", "mobno": "9791077718" },
        "userc": { id: "user id", "ref_code": "..code..", "status": "2", "name": "user_name", "mobno": "9791077718" },
        "usera1": { id: "user id", "ref_code": "..code..", "status": "3", "name": "user_name", "mobno": "9791077718" },
        . . . 
    }
    
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] N/A

------

#### API 09: Generate Referal

<p>
    <a href="https://raw.githubusercontent.com/abbastec/agro/master/08HomeScreenMatrix.JPG" target="_blank">
        <img src="https://raw.githubusercontent.com/abbastec/agro/master/08HomeScreenMatrix.JPG" align="left" width="30" >
    </a>
</p>

Request Type | API End Point
------------ | -------------
GET | http://localhost/agro/api/user/referralcode

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

:Request:
```javascript
{
    "matrix": "A"
}
```

:Response:
```javascript
{
    "status": 1,
    "message": "Ok",
    "referal_code": "37857uefj83u58utfio340895ui930it"
}
```
### Sub Task (Primary)
- [ ] Check for JWT Validity and extract Mobno from JWT and process the request
- [ ] Mobile Number should exist in database and [status=3]
- [ ] Check for Matrix A is available
- [ ] Referal code is hashed with a combination of [mobno /_matrix eg: 9791070918A]

### Sub Task (Secondary)
- [x] No Task

------
