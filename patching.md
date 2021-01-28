# example
``` 
git clone https://github.com/GehirnInc/python-jwt.git # get the orignial code
mv python-jwt python-original_jwt
git clone git@github.com:sajozsattila/python-jwt.git # get the gjwt version
mv python-jwt python-gjwt
cd python-gjwt
git log --pretty=oneline -30 # get the commits too see where we are

cd ../python-original_jwt
git log --pretty=oneline -30 # get the original commits
git format-patch -16 HEAD # get the last 16 commit as patch
cp *.patch ../python-gjwt
cat some.patch | sed "s/jwt/gjwt/g" > some1.patch # replace jwt -> gjwt
mv some1.patch some.patch 
git apply --check  some.patch # test patch is working

git am some.patch # apply patch
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
