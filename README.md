# Meteor Astronomy Security

This module will make it possible for you as a developer to add class and document level
permissions to your Astro classes. 

### Why should you use this package?
Well Astronomy is a great package for enforcing a schema on your mongo collections. You just define what the 
collection schemas are and astronomy will make sure that every document that the app produces conforms to your schema 
definitions. What astronomy doesn't solve yet is who gets to modify the collections.
Sure it does not have to solve this problem as there are numorous patterns and packages that help you with this already.
So why build another one you might ask? What is so unique about this package?
Well a number of things. As you might know if you are using Astronomy the framework is a breaze to work with. It is not a simple 
task it tries to solve but using the framework is very intuitive and effortless. As you also might know if you are a meteor developer with a few apps on your belt, security in meteor is not always very effortless to implement. Allow and deny rules can get really complex very quickly and also can't secure single documents in a collection. Alternative two is securing your app using methods and publications. In my opinion this is the way to go. The only problem with this approach is that it will take much more time to implement. Appart from these two fundamental security patterns you also have to consider what type of security you want to implement. Do you want role based security? Maybe you need private user specific documents or maybe a combination of the two on just a single document. Yes there are many cases to cover, somthing that makes it hard to implement security in a generic and repetable fasion. So finally we arrive at the seed out of which this framework was grown from. <b>The idea is to make a security framework that is simple and generic, secure and flexible as well as ulta cool.</b>

### Features
This package supports securing a collection on a class and document level. You have three security categories: public, roles and user specific. You can set mutiple security controls of different categories for each level. For every control on the class level you can specify insert,update,remove and find rights. For the document level each control can specify read and write rights.

### Let's get down to business

In this part o the readme I will explain how everything works.

#### Security Configuration
Ones you've added the astronomy-security to your meteor app every Astro class except classes without collections will implement a security configuration property. If you want to override the default values in it at initlisation of the astro class you can by providing a security object. This object has three properties that you can set, implementsACL, defaultACL and CLP. You do not need to define these at all if you don't want to as astronomy-security will add this object itself on init. By default the security configuration will not allow anything by anyone.

```javascript
var Comments = new Mongo.Collection('comments');
var Comment = Astro.Class({
  name: 'Comment',
  collection: Comments,
  fields: {
    /*...*/
    }
  },
  security:{
    implementsACL:false,    //optional
    defaultACL: new ACL(),  //optional (read:false, write:false)
    CLP:new CLP()           //optional (insert:false,update:false,remove:false,find:false)
  }

});
```

#### Class Level Permissions (CLP)

