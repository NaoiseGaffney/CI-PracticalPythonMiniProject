<img src="https://codeinstitute.s3.amazonaws.com/fullstack/ci_logo_small.png" style="margin: 0;">

# Code changes:

## The video and sample code has the following that doesn’t work without changes:

```
if __name__ == '__main__':
    app.run(host=os.environ.get('IP'),
            port=int(os.environ.get('PORT')),
            debug=True)
````

Causes an error message: “TypeError: int() argument must be a string, a bytes-like object or a number, not 'NoneType'”.
```
port=int(os.environ.get('PORT')),
```

Remove ‘int’.
```
port=(os.environ.get('PORT')),
```

## The video and sample code has the following that doesn’t work without changes:

```
@app.route('/about')
def about():
    data = []
    with open("data/company.json", "r") as json_data:
        data = json.load(json_data)
    return render_template("about.html", page_title="About", company=data)
````

Causes an error message relating to not finding ‘company.json.
```
with open("data/company.json", "r") as json_data:
```

Adding ‘flask/’ corrects the path.

```
with open("flask/data/company.json", "r") as json_data:
```

## Heroku deployment

1. Create a new repository using the CI Full Template
2. Copy repository link to VS Code and create/select local DropBox repository.
3. Develop Python app with Flask.
4. Test app locally.
5. Add/Commit/Push Project to GitHub using VS Code SCM (Git) or Git CLI.
6. Heroku Web: https://dashboard.heroku.com/apps

    a. Create new app, app name, and region (EU) -> ‘Create app’.
    b. Deploy: ‘GitHub’ (Connect to GitHub) -> Search for a repository to connect to.

7. VS Code Terminal: sudo pip3 freeze --local > requirements.txt

    a. Add/Commit/Push Project to GitHub using VS Code SCM (Git) or Git CLI.

8. Heroku Web: https://dashboard.heroku.com/apps

    a. ‘app’ -> Deploy -> ‘Deploy Branch’
    b. ‘app’…Settings -> ‘Reveal Config Vars’ -> IP 0.0.0.0, PORT 5000

9. VS Code Terminal: echo web: python3 flask/app.py > Procfile 

    a. Add/Commit/Push Project to GitHub using VS Code SCM (Git) or Git CLI.

10. Heroku Web: https://dashboard.heroku.com/apps

    a. ‘app’ -> Deploy -> ‘GitHub’ (Connect to GitHub) -> Deploy Branch
    b. ‘More’ -> Restart all Dynos OR VS Code Terminal: Heroku ps:scale web=1
    c. ‘Open App’
