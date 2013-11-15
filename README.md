DocumentCloud RubyGem
=====================

[![Gem Version](https://badge.fury.io/rb/documentcloud.png)](http://badge.fury.io/rb/documentcloud)

Rubygem for interacting with the DocumentCloud API



## Usage

```gem install documentcloud``` or put in your gemfile and ```bundle install```

then
``` ruby
require 'documentcloud'
```
if not in Rails

To authenticate, initialize the configuration and pass in a block:

``` ruby
DocumentCloud.configure do |config|
  config.email    = 'my_email@somedomain.com'
  config.password = 'my_secret_password'
end
```


### Search

All search results return Document objects that has methods and accessors for the information.

``` ruby
search = DocumentCloud.search('my query')

puts search.total # returns number of results

puts search.documents[0].pdf
```


### Upload

You can upload a document by providing a ruby File object, or a string with the url to a file.

``` ruby
local_doc = DocumentCloud.upload(File.new('/my/file/path.pdf','rb'), 'My Document Title')

remote_doc = DocumentCloud.upload('http://somesite.com/file.pdf', 'Document Title')
```

Both return a document object which can then be used.


## Objects

This gem creates several objects built from the JSON response in order to provide convenience methods and accessors.

### Document

Document objects wrap any document JSON. They are returned in search results, upload, and document methods.

``` ruby
doc = DocumentCloud.document('1234-document-id')

# Accessors
doc.id
doc.title
doc.access
doc.pages
doc.description
doc.source
doc.canonical_url
doc.language
doc.display_langauge

# Methods
doc.pdf               # Full URL to pdf
doc.print_annotations
doc.related_article
doc.text              # Raw parsed text from document
doc.thumbnail         # Primary thumbnail of document

# Images
doc.image(page, size) # Returns the image of a page at the specified size
```

### Search Results
SearchResults objects return information about the search, and an array of Document objects

``` ruby
results = DocumentCloud.search('my query')

results.total    # Total number of results
results.page     # The current results page. Used by specifying page param: DocumentCloud.search('my query', page: 2)
results.per_page # Number of results per page
results.query    # Query string

results.documents # Array of documents of results:

results.documents[0].title # First result title
```



## Information

DocumentCloud API info: http://www.documentcloud.org/help/api