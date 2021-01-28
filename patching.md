# example
``` 
git apply --check  0016-pep8-mypy-compliance.patch # test patch is working

git am 0016-pep8-mypy-compliance.patch # apply patch
```

# Bugfix
If patch not working is possible they are overcommited each other. In this case need to manually fix the files, what we would ike to patch.
```
git apply --check somepatch.patch
```

We will some error like:
```
error: patch failed: gjwt/jwa.py:21
error: gjwt/jwa.py: patch does not apply
error: patch failed: gjwt/jwk.py:41
error: gjwt/jwk.py: patch does not apply
error: patch failed: gjwt/tests/test_jwt.py:83
error: gjwt/tests/test_jwt.py: patch does not apply
error: patch failed: setup.py:24
error: setup.py: patch does not apply
```

Fix up the files manualy regarding to the patch and commi:

```
vi somefile
git add somefile
git commit -m "fix somefile for patch"
git update-index --refresh
git apply --check somepatch.patch
git am somepatch.patch

```
