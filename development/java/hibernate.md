# Hibernate

NB - This information is pretty OLD now.

## Hibernate Tutorial

The First Tutorial I tried was this one from JBoss, it was pretty poor and didnt really even explain the basics
<http://docs.jboss.org/hibernate/core/3.3/reference/en/html/tutorial.html>

I found this one instead which seems better.
<http://pookey.co.uk/wordpress/archives/62-hibernate-with-mysql-a-beginners-guide-part-3>

This one is also good for a few examples of more complex associations
involving more than one table and the ways to initialise and save
multiple objects.
<http://www.metaarchit.com/hibernate_tutorials/Hibernate%20Tutorial%2004.pdf>

And for further reading:
<http://javamug.org/mainpages/presentations/Hibernate-1x2.pdf>
<http://facestutorials.icefaces.org/tutorial/hibernate-tutorial.html#classassociations>

I started off in Netbeans with a Maven project which gave me a quick structure but I had a few issues with the tutorial after that.

- The pom.xml example in the tutorial had no versions for any dependencies which netbeans/builder didn't like at all. Happily I discovered you can add them from the Netbeans menu as dependencies or even edit the pom.xml and add in the <version> tag and it'll give you a list of the available versions in the auto-complete.
- The second issue I had was the way I added the dependencies - the default way of doing it put the dependencies under the <build> element which meant it built fine but while developing none of the classes knew about the dependencies. Solution was to move the <dependencies> tag and contents to outside the build tag. This also made the Netbeans project update the list of libraries available.

### Conclusions

Have a basic tutorial up and running but wasnt too impressed with the
standard of tutorial thats out there. Need to go back and do a
many-to-many and one to many association tutorial too.
