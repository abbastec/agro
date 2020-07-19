### API End Point

#### API: Reset Password
GET: http://localhost/agro/api/user/mobno-login

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
- [ ] If Mobile Number exist in Database and verified, then response status will be 1. We can Navigate the screen to get password.
- [ ] If Mobile Number exist in Database with role admin and not verified, then response status will be 2. We can Navigate the screen to get OTP.
- [ ] If Mobile Number does not exist in Database we will throw 401 error 

### Sub Task (Secondary)
- [ ] Mobile Number Validation [10 numbers]

------

#### API: Request OTP
GET: http://localhost/agro/api/user/request-otp

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "mobno": "979107099"
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
- [ ] Mobile Number should exist in database with status 1 (active)
- [ ] Maximum request per day for a mobile number is 3 (configurable)

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API: Verify OTP
GET: http://localhost/agro/api/user/verify-otp

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
- [ ] Mobile Number should exist in database with status 1 (active)

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API: Login
GET: http://localhost/agro/api/user/login

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
    "password": "Welcome123"
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
    "role": "user",
    "iat": 1593658604,
    "exp": 1593676604
}
```

### Sub Task (Primary)
- [ ] Mobile Number should exist in database with status 1 (active) and already validated with OTP
- [ ] Check for Password Validity
- [ ] Return JWT Token with payload { mobno: 9791070990, role: user or admin or  }

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API: Generate Referal
GET: http://localhost/agro/api/user/referal-register

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
    "mobno": "9791070319", 
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
- [ ] Mobile Number should exist in database with status 3 [Active, Verified, Payment Done]
- [ ] Check for Matrix A is available
- [ ] Referal code is hashed with a combination of [mobno_matrix]

### Sub Task (Secondary)
- [x] No Task

------

#### API: Referal Register
GET: http://localhost/agro/api/user/referal-register

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
    "password": "welcome123",
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
- [ ] Mobile Number should not exist in database with status 1 (active)

### Sub Task (Secondary)
- [x] First name, last name validation. Max Length: 50
- [ ] EMail Id Validation
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation [Min Length 8] [Characters Allowed: A-Z a-z 0-0 _ -] [Must have one alphabet and one number]
- [ ] Validate Referal Code

------

#### API: EMailId Validation
GET: http://localhost/agro/api/user/email-validate

:Header:
```javascript
{
    "Content-Type": "application/json"
}
```

:Request:
```javascript
{
    "code": "sfksdhfkfhhdjfhdsjfhsjf"
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
- [ ] Check for valid code

### Sub Task (Secondary)
- [ ] 

#### API: My Profile
GET: http://localhost/agro/api/user/myprofile

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
    "address": {
        "line1": "address line1",
        "line2": "address line2",
        "landmark": "landmark",
        "city": "city",
        "state": "state",
        "pin": "pin",
    },
    "proof": {
        "panno": "ALRRS9878",
        "panno_url": "...",
        "address_proof_type": "",
        "address_proof_no": "",
        "address_proof_url": "",
        "bank_cross_cheque_url": "",
        "password_leaf_url": "",
        "account_statement_url": "",
    },
    "bank_details": {
        "acno": "123456",
        "ifsc_code": "...",
        "branch": "",
        "city": ""
    }
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
- [ ] Check for JWT Validity
- [ ] Extract Mobno from JWT and process the request

### Sub Task (Secondary)
- [ ] My profile data validation
