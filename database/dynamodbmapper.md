# DynamoDBMapper

DynamoDB low-level API is so WEIRD! The high-level API(DynamoDBMapper) looks more familiar. :P

DynamoDBMapper(Java) is provided by AWS SDK which allows you to map classes to DynamoDB tables. If you have worked with DynamoDB, you know how inconvinient it is to query and parse the result. Part of the reason is that DynamoDB is a key-value store, not a relational database. But with DynamoDBMapper, you can work with DynamoDB table with model classes and do CRUD with ease. The example from the [doc](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBMapper.html):

```java
@DynamoDBTable(tableName="ProductCatalog")
public class CatalogItem {
    
    private Integer id;
    private String title;
    private String ISBN;
    private Set<String> bookAuthors;
    private String someProp;
    
    @DynamoDBHashKey(attributeName="Id")  
    public Integer getId() { return id; }
    public void setId(Integer id) {this.id = id; }
    
    @DynamoDBAttribute(attributeName="Title")  
    public String getTitle() {return title; }
    public void setTitle(String title) { this.title = title; }
    
    @DynamoDBAttribute(attributeName="ISBN")  
    public String getISBN() { return ISBN; }
    public void setISBN(String ISBN) { this.ISBN = ISBN; }
    
    @DynamoDBAttribute(attributeName="Authors")
    public Set<String> getBookAuthors() { return bookAuthors; }
    public void setBookAuthors(Set<String> bookAuthors) { this.bookAuthors = bookAuthors; }
    
    @DynamoDBIgnore
    public String getSomeProp() { return someProp; }
    public void setSomeProp(String someProp) { this.someProp = someProp; }
}
```

This `CatalogItem` will map to `ProductCatalog` table in DynamoDB.

And some of the example CRUD operation are like the following, also from the doc:

```java
AmazonDynamoDB client = AmazonDynamoDBClientBuilder.standard().build();

DynamoDBMapper mapper = new DynamoDBMapper(client);

CatalogItem item = new CatalogItem();
item.setId(102);
item.setTitle("Book 102 Title");
item.setISBN("222-2222222222");
item.setBookAuthors(new HashSet<String>(Arrays.asList("Author 1", "Author 2")));
item.setSomeProp("Test");

mapper.save(item);          
```

For more information, please refer to [DynamoDBMapper documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBMapper.html).

