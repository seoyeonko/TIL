# CRUD
Create, Read, Update, Delete



## Insert
`.save()`

```python
# models.py
from django.db imoprt models

class Person(models.Model):
  SHIRT_SIZES = (
    ('S', 'Small'),
    ('M', 'Medium'),
    ('L', 'Large'),
  )
  nane = models.CharField(max_length=60)
  shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```

```python
# views.py
p = Person(name="Fred Flintstone", shirt_sze="L)
p.save()
```

๐[model ๊ด๋ จ ๊ณต์ ๋ฌธ์](https://docs.djangoproject.com/ko/3.2/topics/db/models/)     
๐[crud ๋ช๋ น์ด ๊ด๋ จ ๊ณต์ ๋ฌธ์](https://docs.djangoproject.com/ko/3.2/topics/db/queries/)

```html
<!-- Django Template Language -->

{% for member in total_member %}
	์์ด๋ : {{ member.userid }}<br>
	์ด๋ฆ : {{ member.username }}<br>
{% endfor %} <!-- ๋ฐ๋ณต๋ฌธ์ ๋ง์ง๋ง ์์น๋ฅผ ์๋ ค์ค: ์์ฑํด์ฃผ์ด์ผ for๋ฌธ ์์ฑ --> 
```

<br>

## Update
๋ณ๊ฒฝํ  ๊ฒ์ ๋ณ๊ฒฝํ ํ์ `.save()`

```python
member = Member.objects.filter(userid="haha")

print(member.userid) # haha
print(member.username) # ํ๊ธธ๋

# id: ํํ
# name: ํ๊ธธ๋
# username = "์ฑ์ถํฅ" 

member.save()
```

- PK (Primary Key, ์ฃผ ํค)
    - ํ๋์ ๋ ์ฝ๋๋ฅผ **๋ค๋ฅธ ๋ ์ฝ๋์ ์๋ณํ๊ฒ ํด์ฃผ๊ธฐ ์ํ "๊ณ ์ ๊ฐ"**  
    - **์ฐ์์ ์ธ ์ซ์**๋ก ํ๋ ๊ฒ์ด ์ผ๋ฐ์ ์ 

    DB์์ CRUD๋ฅผ ์ฒ๋ฆฌํ  ๋ ๋ด๋ถ์ ์ผ๋ก pk๋ฅผ ์ด์ฉํด ๋ง์ ๊ฒ์ ํจ! 
    โ pk๋ฅผ ์ด์ฉํด ์กฐํ, ์ญ์  ๋ฑ์ ์์์ ์งํ

    Django๋ DB๋ฅผ ํฌํจํ๊ธฐ์ pk๋ฅผ ๋ฐ๋ก ์ง์ ํ  ํ์๊ฐ ์์! 

### **[filter() vs. get() ์ฐจ์ด์ ](https://stackoverflow.com/questions/3221938/difference-between-djangos-filter-and-get-methods)**
- `filter()`
    - QuerySet์ ๋ฐํ
- `get()`
    - Object ๋ฐํ
    - ๊ฐ์ง๊ณ ์ฌ ๋ฐ์ดํฐ๊ฐ ํ๋๋ง ์์์ ๋ณด์ฅํ  ๋ ์ฌ์ฉ
โ Basically use `get()` when you want to get **a single unique object**, and `filter()` when you want to get **all objects** that match your lookup parameters.

### ๋น๋ฐ๋ฒํธ ๋ณ๊ฒฝ ์์ 
```python
(...)

# ๋ก๊ทธ์ธ
def login(req):
    # get() ์ด์ฉํด ์ ๋ณด๋ฅผ ๋ณ๊ฒฝํ๊ณ ์ ํ๋ "ํน์  user"๋ฅผ ๊ฐ์ ธ์ด 
    user = User.objects.get(userid="cherry1)
    # ๋น๋ฐ๋ฒํธ ๋ณ๊ฒฝ
    user.password="2345 # password: User Model์ password ์์ฑ์ ์๋ฏธ 
    user.save # DB์ ์ ์ฅ
    
    return render(req, 'login.html')
```

`delete()`, `save()` ๋ฌธ์ ํ ๊ฐ์ฒด์ ๋ํด์๋ง ์คํ์ด ๊ฐ๋ฅํจ 
  - โญ๏ธ user๊ฐ **object**์ด์ด์ผ ์ ์์ ์ผ๋ก ์คํ
  - โ **queryset**์ด๋ฉด ์๋จ     
โ **ํจ์์ ์คํ ๋์์ด ํ๋๋ง ์กด์ฌ**ํด์ผ ํ๋ค๋ ์๋ฏธ      

๐ [ref](https://stackoverflow.com/questions/9143262/delete-multiple-objects-in-django) (stackoverflow) - ๋ณต์ ๊ฐ์ ๋ฐ์ดํฐ๋ฅผ deleteํ๋ ๋ฐฉ๋ฒ! 
```python
Post.objects.all().delete()
Post.objects.filter(pup_date__gt=datetime.now()).delete()
```

<br>

## DELETE
`.delete()`

```python 
def signout(req):
    # get() ์ด์ฉํด ์ ๋ณด๋ฅผ ๋ณ๊ฒฝํ๊ณ ์ ํ๋ "ํน์  user"๋ฅผ ๊ฐ์ ธ์ด 
    user = User.objects.get(userid="cherry1)

    # ํ์ ํํด
    user.delete()
    
    return render(req, 'signout.html)
```


<br>


# ORM, QuerySet

## QuerySet
์ ๋ฌ๋ฐ์ ๋ชจ๋ธ์ ๊ฐ์ฒด ๋ชฉ๋ก โ DB๋ก๋ถํฐ ๋ฐ์ดํฐ๋ฅผ ์ฝ๊ณ , ํํฐ๋ฅผ ๊ฑธ๊ฑฐ๋ ์ ๋ ฌ ์์ ๊ฐ๋ฅ			

Django Shell์ ์ด์ฉํ ์ค์ต		
`python3 manage.py shell`: Django Shell ์คํ ๋ช๋ น์ด


(User ๋ชจ๋ธ์ ์์ฑํ๋ค๋ ๊ฐ์ )
- `>>> from user.models import User`
    - User ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํด ๋ชจ๋ธ์ ๋ถ๋ฌ์์ผ ํจ 

- `>>> User.objects.all()`
    - ๋ชจ๋  ๊ฐ์ฒด ์กฐํ 

- `>>> User.objects.create(userid='4',username='ํ์คํธ4',password='d',gender='M')`
    - ์๋ก์ด ๊ฐ์ฒด ์์ฑ โ ๊ฐ์ฒด๋ฅผ ์๋ก ๋ง๋ค ๋, ๋ชจ๋  ์์ฑ๊ฐ๋ค์ ์ค์ ํด์ผ ํจ 

- `>>> User.objects.filter(gender='W')`
    - ํํฐ๋ง (์ฑ๋ณ์ด ์ฌ์์ธ ๊ฐ์ฒด ํํฐ๋ง)

- `>>> User.objects.order_by('registered')` - ์ค๋ฆ์ฐจ์
- `>>> User.objects.order_by('-registered')` - ๋ด๋ฆผ์ฐจ์ (ํ๋๋ช ์์ `-`)
    - ์ ๋ ฌ (๋ฑ๋ก ์๊ฐ์ ๊ธฐ์ค์ผ๋ก ์ ๋ ฌ)

- `exit()`
    - ์ฅ๊ณ  shell ์ข๋ฃ



