# Serenity/JS Cucumber API Testing

Issue:
```
When he wants to create a new message with author J.R.R. Tolkien and message The Lord of the Rings
[test:execute]     ☕ImplementationPendingError: Step implementation missing:
[test:execute] 
[test:execute]     When('{pronoun} wants to create a new message with author J.R.R. {actor} and message {actor} {actor} of the {actor}', function (pronoun, actor, actor2, actor3, actor4) {
[test:execute]       // Write code here that turns the phrase above into concrete actions
[test:execute]       return 'pending';
[test:execute]     });
[test:execute]   ⇢ Then he is able to create the new message
[test:execute] 
[test:execute] ☕Implementation pending (56ms)
[test:execute] 
[test:execute]   ImplementationPendingError: Step implementation missing:
[test:execute] 
[test:execute]   When('{pronoun} wants to create a new message with author J.R.R. {actor} and message {actor} {actor} of the {actor}', function (pronoun, actor, actor2, actor3, actor4) {
[test:execute]     // Write code here that turns the phrase above into concrete actions
[test:execute]     return 'pending';
[test:execute]   });
[test:execute] ================================================================================
[test:execute] Execution Summary
[test:execute] 
[test:execute] DEMO_RESTAPI: 1 pending, 1 total (56ms)
[test:execute] 
[test:execute] Total time: 56ms
[test:execute] Scenarios:  1
[test:execute] ===========================================================================
```

Fix:
```
  Examples:
      | author | message | 
      | "J.R.R. Tolkien" | "The Lord of the Rings" | 

```

Note
```
https://cucumber.io/docs/cucumber/cucumber-expressions/#parameter-types
```

Issue #2
```
test:execute]     ✗ James ensures that a Promise does equal 'Curry Blake' (1ms)
[test:execute] 
[test:execute]       Difference (+ expected, - actual):
[test:execute] 
[test:execute]       - a Promise
[test:execute]       + 'Curry Blake'
[test:execute] 
```

try with 
 Log.the(Property.of(LastResponse.body<MessageDto>()).author.answeredBy(actor)),
 get back:
 ```
 ✓ James logs: a Promise (0ms)
[test:execute]       a Promise:
[test:execute]       'Curry Blake'
```

How to share state between steps?
Using TakeNotes

 ConfigurationError: James can't TakeNotes yet. Did you give them the ability to do so?

  
  Fix: 
  TakeNotes.usingAnEmptyNotepad()

The usingAnEmptyNotepad is a function!

Note.of to retrieve the data "author" does not work
```
Log.the(Note.of('author')),
Log.the(Note.of(q`$(author)`)), 
```  
both does not work

Fix:
  TakeNote.of(
        Question.about<string>(`Author`, actor => {
          return author; // Actual value
        })
      ).as('Author'),


  Log.the(Note.of('Author')),


  Issue:
  ```
  test:report] Aug 16, 2023 1:11:14 PM com.google.inject.internal.MessageProcessor visit
[test:report] INFO: An exception was caught and reported. Message: java.lang.reflect.InaccessibleObjectException: Unable to make protected final java.lang.Class java.lang.ClassLoader.defineClass(java.lang.String,byte[],int,int,java.security.ProtectionDomain) throws java.lang.ClassFormatError accessible: module java.base does not "opens java.lang" to unnamed module @1e643faf
[test:report] java.lang.IllegalStateException: Unable to load cache item
[test:report]   at com.google.inject.internal.cglib.core.internal.$LoadingCache.createEntry(LoadingCache.java:79)
[test:report]   at com.google.inject.internal.cglib.core.internal.$LoadingCache.get(LoadingCache.java:34)
[test:report]   at com.google.inject.internal.cglib.core.$AbstractClassGenerator$ClassLoaderData.get(AbstractClassGenerator.java:119)
[test:report]   at com.google.inject.internal.cglib.core.$AbstractClassGenerator.create(AbstractClassGenerator.java:294)
[test:report]   at com.google.inject.internal.cglib.reflect.$FastClass$Generator.create(FastClass.java:65)


```

Info
```
java --version
openjdk 17.0.6 2023-01-17
OpenJDK Runtime Environment (build 17.0.6+0-17.0.6b802.4-9586694)
OpenJDK 64-Bit Server VM (build 17.0.6+0-17.0.6b802.4-9586694, mixed mode)
a845751yara.com@Lays-MBP-2 serenityjs-rest % 
```
