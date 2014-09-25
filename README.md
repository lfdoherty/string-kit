

# String Kit

A string manipulation toolbox.

* License: MIT
* Current status: early alpha
* Platform: Node.js only (browser support is planned)



# Install

Use Node Package Manager:

    npm install string-kit





Full BDD spec generated by Mocha:


# TOC
   - [format()](#format)
<a name=""></a>
 
<a name="format"></a>
# format()
%u should format unsigned integer.

```js
expect( format( '%u' , 123 ) ).to.be( '123' ) ;
expect( format( '%u' , 0 ) ).to.be( '0' ) ;
expect( format( '%u' , -123 ) ).to.be( '0' ) ;
expect( format( '%u' ) ).to.be( '0' ) ;
```

%U should format *positive* unsigned integer.

```js
expect( format( '%U' , 123 ) ).to.be( '123' ) ;
expect( format( '%U' , 0 ) ).to.be( '1' ) ;
expect( format( '%U' , -123 ) ).to.be( '1' ) ;
expect( format( '%U' ) ).to.be( '1' ) ;
```

should.

```js
expect( format( 'ABC: %s%s%s' , 'A' , 'B' , 'C' ) ) ;
expect( format( 'BAC: %+1s%-1s%s' , 'A' , 'B' , 'C' ) ) ;
expect( format( 'CBC: %3s%s' , 'A' , 'B' , 'C' ) ) ;
```

format.count() should count the number of arguments found.

```js
expect( format.count( 'blah blih blah' ) ).to.be( 0 ) ;
expect( format.count( '%i %s' ) ).to.be( 2 ) ;
```

when using a filter object as the *this* context, the %[functionName] format should use a custom function to format the input.

```js
var filters = {
	fixed: function() { return 'F' ; } ,
	double: function( str ) { return '' + str + str ; } ,
	fxy: function( a , b ) { return '' + ( a * a + b ) ; }
} ;

expect( format.call( filters , '%[fixed]%s%s%s' , 'A' , 'B' , 'C' ) ).to.be( 'FABC' ) ;
expect( format.call( filters , '%s%[fxy:%a%a]' , 'f(x,y)=' , 5 , 3 ) ).to.be( 'f(x,y)=28' ) ;
expect( format.call( filters , '%s%[fxy:%+1a%-1a]' , 'f(x,y)=' , 5 , 3 ) ).to.be( 'f(x,y)=14' ) ;
```

