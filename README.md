How to get start?
```
./startwebserver.sh
```

```
yarn test:stage
```

test report is available at 
```
http://serenitybdd.s3-website-ap-southeast-1.amazonaws.com/
```


CircleCI config
```
As a best practice, it is generally recommended for your cache strategy 
to checksum on the package-lock.json file, 
rather than the package.json file. 
This is because, based on the way you declare version requirements on your Node dependencies, 
the package-lock.json file reflects better if changes to required dependencies are updated.
```
