

## Comparison Operators

Comparison operators are used to compare values in a query. Some common comparison operators include:
- `$eq`: Matches values that are equal to a specified value.
- `$gt`: Matches values that are greater than a specified value.
- `$lt`: Matches values that are less than a specified value.
- `$gte`: Matches values that are greater than or equal to a specified value.
- `$lte`: Matches values that are less than or equal to a specified value.
- `$ne`: Matches all values that are not equal to a specified value.
- `$in` : Matches any of the values specified in an array.

*Dataset Name:* `bank.sales.csv`)
### Find one document where Value is greater than 100000
 
db.sales.findOne({ Value: { $gt: 100000 } })
 

### Find Number of documents where Transaction_count is less than or equal to 1000
 
db.sales.find({ Transaction_count: { $lte: 1000 } }).count()
 

### Find Number of documents where Location is an array containing 'Mumbai'
 
db.sales.find({ Location: { $in: ['Mumbai' , 'Pune'] } }).count()
 
## Logical Operators



### Find documents where Location is 'Mumbai' or 'Delhi' using logical operators
 
db.sales.find({ $or: [ { Location: 'Mumbai' }, { Location: 'Delhi' } ] })
 

### Find documents where Domain is 'RETAIL' and Location is 'Pune' using logical operators
 
db.sales.find({ $and: [ { Domain: 'RETAIL' }, { Location: 'Pune' } ] })
 

## Element Operators



### Find documents where Transaction_count does not exist
 
db.sales.find({ Transaction_count: { $exists: false } })
 

### Find documents where the 'Value' field is of type number (double)
 
db.sales.find({ Value: { $type: 'double' } })
 
    
### Find Number of documents where Domain exists
 
db.sales.find({ Domain: { $exists: true } }).count()
 