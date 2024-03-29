# Customizable Django Profiler (Not Maintained anymore)

Django cProfile middleware having configurable triggers and outputs

## Requirements

Django-1.10 or above (For below version 1.10 refer this [package](https://github.com/lavi06/django-profile-middleware))

## Getting Started

Follow given instructions to setup customizable-django-profiler

### Install

Install via pip

```bash
$ pip install customizable-django-profiler
```

### Add
Add `customizable_django_profiler.cProfileMiddleware` to the end of `MIDDLEWARE` in project's `settings.py`

```bash
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    ....
    'customizable_django_profiler.cProfileMiddleware',
]
```
### Enable
Add `PROFILER` in project's `settings.py` and set `activate = True`.

```bash
PROFILER = {
    'activate': True,
}

```
Done!
This will provide the profile data on the server console

Example

```bash
        622 function calls (579 primitive calls) in 0.001 seconds

   Ordered by: internal time
   List reduced from 207 to 100 due to restriction <100>

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
   ...      ...      ...       ...     ...           ...
   ...      ...      ...       ...     ...           ...

   ```

## Customize

You can customize the Profiler settings via adding some varaibles in `Profiler` key in `settings.py`

Default are

```bash
PROFILER = {
    'activate': True,
    'sort': 'time',
    'count': '100' ,
    'output': ['console'],             
    'file_location': 'profile.txt',
    'trigger': 'all'
}
```
Description of cutomizable keys
### activate
Set this key to `True` to enable Profiler

```bash
'activate': True
```
To disable set to `False`
```bash
'activate': False
```

### sort
Sort according to the set value. Default is `'time'`.
See [documentaion](http://docs.python.org/2/library/profile.html#pstats.Stats.sort_stats) for more options

### count
Specify number of rows to output. Default is `100`.

### output
Specify the form of output. Multiple output formats can be selected. Default is `['console']`. Options are `'file'`, `dump` and `'response'`.  
`'file'` and `dump` will write the file specified by `'file_location'` key and `'response'` will output the result as response of request.  
`file` is used for a txt file.  
`dump` will be used for binary dump.  
Some examples are

```bash
'output': ['console']
```
```bash
'output': ['console', 'file', 'response']
```
```bash
'output': ['file', 'response']
```

### file_location
Specify the location of file you want to write in the results. **Only valid if `'file'` in `'output'` key**. Default value `profile.txt`

### trigger
Specify the trigger for API on which profiler runs. Default is `'all'`. Instead you can trigger profiler by passing a query parameter, which can be specified after `:` in `'trigger'` key for example

```bash
'trigger' : 'query_param:profile'
```

Profiling will only be enabled for APIs with `profile` in their request parameters.

```bash
http://localhost:8000/api/?profile
```

## Author

* [Somesh Chaturvedi](https://github.com/someshchaturvedi)

## Contibutors

* [José L. Redrejo Rodríguez](https://github.com/jredrejo)

## License

This project is licensed under the [MIT](LICENSE.md).
