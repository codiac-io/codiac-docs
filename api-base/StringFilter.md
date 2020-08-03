# StringFilter Operators


The StringFilter type provides some convenient search syntaxes, and the best part is that they're built in, so you wont have to write any custom code to support them. 

Just prefix your value with an operator and an underscore `'_'` 

```url
shoes?brand=$sw_ree
```

This will return all shoes with brand names starting with the letters `"ree"` (like Reebok).    *All StringFilter searches are ***case-INsensitive***.*

You can invoke these behaviors by applying the following operators to your value 
* [StartsWith](#StartsWith): `$sw_` or `startswith_`
* [EndsWith](#EndsWith): `$ew_` or `endswith_`
* [Contains](#Contains): `$cn_` or `contains_`
* [In List](#In): `$in_` or `in_`
* [RegEx Pattern](#Pattern): `$pn_` or `pattern_`
* [Equals](#Equals): `$eq_` or `equals_`

***AND***

All of these operators can also be inversed with the [`NOT` operator: `!`](#Not) 

## <a name='StartsWith'></a> The `StartsWith` Operator
To search on string properties that **start with** a given value *(eg: "N" to find "Nike" and "New Balance")*, prefix your value with `$sw_` or `startswith_`:
```url
shoes?brand=$sw_N
or
shoes?brand=startswith_N
``` 

NOTE:  *All StringFilter prefixes such as these are NOT case-sensitive, so `?StartsWiTH_N` will work just as well as `?startswith_N` or `?$SW_N`.*

You can also invoke the [Not operator](#Not): `!$sw_` or `!startsWith_`

## <a name='EndsWith'></a> The `EndsWith` Operator

To search on string properties that **end with** a given value *(eg: "e" to find "Nike" and "New Balance")*, prefix your value with `$ew_` or `endsswith_`:
```url
shoes?brand=$ew_e
or
shoes?brand=endswith_e
``` 

You can also invoke the [Not operator](#Not): `!$ew_` or `!endsWith_`

## <a name='Contains'></a> The `Contains` Operator

To find strings that contain a given value *(eg: "ok" to find "Brooks" and "Reebok")* prefix your value with `$cn_` or `contains_`:
```url
shoes?brand=$cn_ok
or
shoes?brand=contains_ok
```

You can also invoke the [Not operator](#Not): `!$cn_` or `!contains_`

## <a name='In'></a> The `In` Operator

Whereas a simple equals operator limits results to those matching a single value, the `$in` operator allows you to limit results to those matching one of several values.  
That is, if you want not only Nike shoes but Brooks and Asics too, pass all three brands as your value (separated by commas) and prefix the whole thing with `$in_` or `in_`: 

```url
shoes?brand=$in_Nike,Brooks,Asics
or
shoes?brand=in_Nike,Brooks,Asics
```

This syntax employs "OR" logic:  where brand equals "Nike" OR "Brooks" OR "Asics" 

You can also invoke the [Not operator](#Not): `!$in_` or `!in_`


## <a name="Pattern"></a> The `Pattern` Operator

RegExes anyone? (aka: Regular Expressions, aka: string patterns)  If you want to search on values that conform to a more complex set of rules, you can pass in a [regular expression](https://regexr.com/) as your value and prefix it with the `pattern` operator or `$pn`:

let's say we want shoes whose brands have two words in their name:

```RegExp
/\w+\s\w+/   
```

```
Url-encoded:  %2F%5Cw%2B%5Cs%5Cw%2B%2Fi
```


*NOTE: Obviously special characters could be trouble here, so always be sure to [Url-encode](https://meyerweb.com/eric/tools/dencoder/) your values before adding them to the querystring*

```url
shoes?brand=$pn_%2F%5Cw%2B%5Cs%5Cw%2B%2Fi
or
shoes?brand=pattern_%2F%5Cw%2B%5Cs%5Cw%2B%2Fi
```

NOTE:  *Yes, we url-encoded before prefixing instead of url-encoding the whole value, but it's legal to do so because the prefixes are made up of legal URL characters that do not need encoding (via [RFC3986](https://www.ietf.org/rfc/rfc3986.txt) and [RFC1738](https://www.ietf.org/rfc/rfc1738.txt)).*

You can also invoke the [Not operator](#Not):  `!$pn_` or `!pattern_`

## <a name='Equals'></a> The `Equals` Operator

*You may never use this because it's already the default behavior of a search string that is not prefixed with an operator.*

```
shoes?brand=nike
```

But if you felt the need to explicitly call it out, you can instead prefix your value with `$eq_` or `equals_`:
```url
shoes?brand=$eq_nike
or
shoes?brand=equals_nike
``` 

You can also invoke the [Not operator](#Not):  `!$eq_` or `!equals_`

## <a name='Not'></a> The `Not` Operator

The Not operator (`!`) exists as an optional prefix that you can apply to the other operators, which inverts their logic to include anything NOT MATCHING their logic.

For example, If you want all shoes other than "Nike", you can prefix the `Equals` operator with the `Not` operator:

```url
shoes?brand=!$eq_nike
or
shoes?brand=!equals_Nike
```

And in case you were wondering, there is NO NEED to url-encode the `!` exclamation point.  The Internet Engineering Task Force (IETF) clearly defined it as a safe character in:
* [RFC3986: Uniform Resource Identifier (URI): Generic Syntax](https://www.ietf.org/rfc/rfc3986.txt)
* [RFC1738: Uniform Resource Locators (URL)](https://www.ietf.org/rfc/rfc1738.txt)
 
