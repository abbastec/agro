### API End Point
#### API 01: Referal Register
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
    "last_name": "Perumal;",
    "email": "senthil@gmail.com",
    "mobno": "9791078777",
    "password": "welcome123"
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

### Sub Task (Secondary)
- [x] First name, last name validation. Max Length: 50
- [x] EMail Id Validation
- [x] Mobile Number Valdiation [Number Only] [Max Length 10]
- [x] Password Validation [Min Length 8] [Characters Allowed: A-Z a-z 0-0 _ -] [Must have one alphabet and one number]
- [x] Mobile Number should not exist in database with status 1 (active)
