# Creating a phone book with Python
Each user's information is as follows:
* name
* email
* adresss
* id 
---
Features of this phone book:
* Add user
* Read phonebook users
* Edit user
* Delete user
---
### Required libraries
* json
* os
### How to install Jason library
We write in the terminal
```python
pip install jason
```
### How to install os library
We write in the terminal
```python
pip install os
```
---
## Start building the program
step one: import libraries
```python
import json
import os
```
### Creating a list to put users in it
```python
phoonebook=[]
```
### Creating a function to load the file and close it
```python
def load():
    o=open('telephon.json','r')
    p = json.loads(o.read())
    o.close()
    return p
```
### Create a function to write to the json file
```python
def write():
    o=open('telephon.json','w')
    o.write(json.dumps(phoonebook))
    o.close()
```
### Create function to add user
Each user has a unique ID so that we can identify them in the list

```python
def add_user():
    name=input('enter your new name: ')
    numper=input('enter your new number: ')
    email=input('enter your new email: ')
    address=input('enter your new adress: ')
    user={"name":name,"number":numper,"email":email,"address":address}
    id=1
    if len (phoonebook)==0:
        user['id']=1
    else:
        id=max(i['i']for i in phoonebook)
    user['id']=id
    phoonebook.append(user)
    write()
    print(f'your user saved with id {id}')
```
### A function to read all users and their information
```python
def read():
    for i in phoonebook:
        print(f"id:{i['id']},name={i['name']},number={i['number']},email={i['email']},address={i['address']}")
```
### Function to edit user information
Each user is identified by an ID
```python

def update():
    id=int(input('enter your id user: '))
    for user in phoonebook:
        if user['id']==id:
            order=int(input('enter your part:1=name  ,2=number  ,3=email  ,4=address  '))
            if order==1:
                user['name']=input('enter update name: ')
               
            elif order==2:
                user['number']=input('enter update number: ')
                
            elif order==3:
                user['email']=input('enter your update email: ')
                
            elif order==4:
                user['address']=input('enter your update address: ')
            else:
                print('your order invalid')
                
            write()
        else:
            print('your id is invalid')
```
### Delete user function

```python
def delet():
    id=int(input('enter your user id: '))
    for i in range(len(phoonebook)):
        if phoonebook[i]['id']==id:
            del phoonebook[i]
            print('thats remove it')
            write()
            return
    print('not found it')
```
### Add the json file to the list if it exists

```python
if os.path.exists('telephon.json'):
    phoonebook = load()
```
### Making a loop to put the functions inside

```python
while(True):
    print('enter your optione\n1=add user\n2=read phone book\n3=updatr user\n4=delet user\n5=exit')
    choice=input('enter your choice:')
    if choice=='1':
        add_user()
    elif choice=='2':
        read()
    elif choice=='3':
        update()
    elif choice=='4':
        delet()
    elif choice=='5':
        break
    else:
        print('your number invaild please try again')
```