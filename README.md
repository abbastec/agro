### API End Point

#### API 01: Mobile Number Login
POST: http://localhost/agro/api/user/mobno-login

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
- [ ] If Mobile Number exist in Database and [Status=2 or Status=3], then response status will be 1. We can Navigate the screen to get password.
- [ ] If Mobile Number exist in Database and [Status=1], then response status will be 2. We can Navigate the screen to get OTP. Also API will send Generated OTP to mobile number. 
- [ ] If Mobile Number does not exist in Database we will throw 401 error 

### Sub Task (Secondary)
- [ ] Mobile Number Validation [10 numbers]
- [ ] Maximum OTP request for a mobile number is 3 [configurable] per day

------

#### API 02: Validate OTP and Set New Password
POST: http://localhost/agro/api/user/validate-otp-set-password

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

#### API 03: Request EMmail Verification Link
POST: http://localhost/agro/api/user/request-email-verify-link

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
- [ ] Mobile Number should exist in database and [status = 2]
- [ ] send a password hashed value as a link to the registered email.


### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API 04: Validate EMailID
GET: http://localhost/agro/api/user/validate/6thtrhy566756765y567

:Header:
```javascript
{
    "Content-Type": "application/json"
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
- [ ] Verify EMail Code and check User [status =2]

### Sub Task (Secondary)
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]

------

#### API 05: Login with Password
POST: http://localhost/agro/api/user/login

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

#### API 06: My Profile
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
- [ ] My profile form data validation

------

#### API 07: Payment
GET: http://localhost/agro/api/user/payment

:Header:
```javascript
{
    "Content-Type": "application/json"
    "Authorization": "jwt token..."
}
```

### Sub Task (Primary)
- [ ] Check for JWT Validity
- [ ] Extract Mobno from JWT and process the request
- [ ] Analysis needed. For test purpose we can make a entry in payment table

### Sub Task (Secondary)
- [ ] N/A

------

#### API 08: Generate Referal
GET: http://localhost/agro/api/user/generate-referal

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
- [ ] Mobile Number should exist in database and [status=3]
- [ ] Check for Matrix A is available
- [ ] Referal code is hashed with a combination of [mobno_matrix eg: 9791070918_A]

### Sub Task (Secondary)
- [x] No Task

------

#### API 09: Register with Referal Code
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

### Sub Task (Secondary)
- [ ] First name, last name validation. Max Length: 50
- [ ] EMail Id Validation
- [ ] Mobile Number Valdiation [Number Only] [Max Length 10]
- [ ] Password Validation [Min Length 8] [Characters Allowed: A-Z a-z 0-0 _ -] [Must have one alphabet and one number]
- [ ] Validate Referal Code

------
