# XML - should merge with webservices

- [XML - should merge with webservices](#xml---should-merge-with-webservices)
  - [JEE tutorials on XML](#jee-tutorials-on-xml)
    - [Using StaX](#using-stax)
      - [JAXB - XML binding in Java](#jaxb---xml-binding-in-java)
      - [Display xml node as a string](#display-xml-node-as-a-string)

## JEE tutorials on XML

J2EE 1.4 tutorial has sections on XML and APIs including SAX, DOM, JAXP.

Basic Parsing and XPath examples:

- <http://www.kdgregory.com/index.php?page=xml.parsing>
- <http://www.kdgregory.com/index.php?page=xml.xpath>

### Using StaX

<http://www.devx.com/Java/Article/30298/0/page/3>

#### JAXB - XML binding in Java

To get some nice objects that you can marshall or unmarshall here are some tips.

- Generate an XSD if you just have a plain XML example file.

```bash
 /Dev/Java/Libraries/xmlbeans-2.5.0/bin/inst2xsd test01.xml
```

- Use your XSD along with a binding file to generate some Java objects via the XJC compiler
- XJC is included with the Java6 install in the /bin directory.
- It can be invoked on the command line but can also (using an extra jar) be incorporated into an ANT task.

```bash
  xjc -b binding.xml -p com.yourcompany.generated test_0.xsd
```

#### Display xml node as a string

All stuff is part of Java implem.

```java
      Document document = doc.getDocumentElement().getOwnerDocument();
      DOMImplementationLS domImplLS = (DOMImplementationLS)document.getImplementation();
      LSSerializer serializer = domImplLS.createLSSerializer();
      String str = serializer.writeToString(doc);
      System.out.println(str);
```
