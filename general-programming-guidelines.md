# Programming Guidelines

This programming guideline contains standard conventions that are/will be used in yetu. The goal is to produce high quality applications which has a same coding conventions and coding style. Examples that are placed in this language is in Java language, however most of the rules can be used in any language and some of the rules are only for object-oriented programming languages. Therefore please use this guideline as part of your development process.

Some of the common code style conventions are not included in this document (e.g. indentation or max. number of line in file), because current Integrated development environments(IDE) are advance enough to provide features that developers do not have to  worry about it.


## 1. Programming Principles

### Class Design
1. **The Single Responsibility Principle** : A class should have one, and only one, reason to change. [1][ref-1]

2. **The Open Closed Principle** : You should be able to extend a classes behaviour, without modifying it. [2][ref-2]

3. **The Liskov Substitution Principle** : Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it. [3][ref-3]

4. **The Interface Segregation Principle** : Make fine grained interfaces that are client specific, meaning no client should be forced to depend on methods it does not use. [4][ref-4]

5. **The Dependency Inversion Principle** : Depend on abstractions, not on concretions. [5][ref-5]


###Package Cohesion

1. **The Release Reuse Equivalency Principle** : The package must be created with reusable classes — “Either all of the classes inside the package are reusable, or none of them are.[6][ref-6]

2. **The Common Closure Principle** : Classes that change together are packaged together. [6][ref-6]

3. **The Common Reuse Principle** : Classes that are used together are packaged together. [6][ref-6]


###Package Coupling
Packages can be decoupled by separating their responsibility, and they can be turn into the releasable packages such as simple software libraries (e.g. jar file with maven).

1. **The Acyclic Dependencies Principle** : The dependency graph of packages must have no cycles, meaning each component that is can be separated from the rest of the system, it should be developed and build separately. [6][ref-6]

2. **The Stable Dependencies Principle** : Depend in the direction of stability. A package should only depend upon packages that are more stable than it is.  [7][ref-7]

3. **The Stable Abstractions Principle** : Abstractness increases with stability. [7][ref-7]



## 2. Code Style
###Naming Conventions
1. All names should be written in English names. 

2. Use searchable names.

3. Don’t be cute.
         
        kill(); 	// NOT: whack(); 
        abort(); 	// NOT: goodbye();
         

4. Names representing packages should be in all lower case.

 
        mypackage, com.yetu.app.ui, de.company.application

5. Names representing types must be nouns and written in mixed case starting with upper case.
		
		Line, AudioSystem

6. Variable names must be in mixed case starting with lower case.
	
		line, audioSystem

7. Names representing constants (final variables) must be all uppercase using underscore to separate words.
       
        MAX_ITERATIONS, COLOR_RED

8. Names representing methods must be verbs and written in mixed case starting with lower case.

        getName(), computeTotalWidth()

9. Abbreviations and acronyms should not be uppercase when used as name.

        exportHtmlSource(); // NOT: exportHTMLSource();
        openDvdPlayer();    // NOT: openDVDPlayer();


10. Generic variables should have the same name as their type.

        void setTopic(Topic topic); 
        
        // NOT: void setTopic(Topic value);
        // NOT: void setTopic(Topic aTopic);
        // NOT: void setTopic(Topic t);

        void connect(Database database);
        // NOT: void connect(Database db);
        // NOT: void connect(Database oracleDB)

        Furthermore, to avoid name confusion of class variable and method variable argument, variables can have prefix (e.g. new).

        void setTopic(Topic newTopic);

11. The name of the object is implicit, and should be avoided in a method name.
        
        line.getLength();   // NOT: line.getLineLength();


12. The terms *get/set* must be used where an attribute is accessed directly.
        
        employee.getName();
        employee.setName(name);

        matrix.getElement(2, 4);
        matrix.setElement(2, 4, value);
        
13. *is* prefix should be used for boolean variables and methods.
        
        isSet, isVisible, isFinished, isFound, isOpen

14. Plural form should be used on names representing a collection of objects.
        
        Collection<Point>  points;
        int[]              values;

15. Complement names must be used for complement entities.

        get/set, add/remove, create/destroy, 
        start/stop, insert/delete,
        increment/decrement, old/new, begin/end, 
        first/last, up/down, min/max,
        next/previous, old/new, open/close, 
        show/hide, suspend/resume, etc.

16. Abbreviations in names should be avoided.

        computeAverage();               	// NOT: compAvg();
        ActionEvent event;             	// NOT: ActionEvent e;


17. Negated boolean variable names must be avoided.


        bool isError; // NOT: isNoError
        bool isFound; // NOT: isNotFound

18. Associated constants (final variables) should be in a separate class.

		public class Color {
        	static final int COLOR_RED   = 1;
        	static final int COLOR_GREEN = 2;
        	static final int COLOR_BLUE  = 3;
       }
	
	or
	
		public enum Color {
        	RED, GREEN, BLUE
        }

###Programming Practice Conventions
1. Numerical constants (literals) should not be coded directly, except for -1, 0, and 1, which can appear in a for loop as counter values.

        1000 * 60 * 60 * 24; 	//WRONG 
        // should be
        static final int MILLISECOND = 1;
        static final int SECOND = MILLISECOND * 1000;
        static final int MINUTE = SECOND * 60;
        static final int HOUR = MINUTE * 60;
        static final int DAY = HOUR * 24;


##3.Code Comment

1. Comments do not make up for bad code.

2. Explain yourself in code.

        // Check to see if the employee is eligible for full benefits 
        if ((employee.flags & HOURLY_FLAG) &&
        (employee.age > 65))
        
        Or

        if (employee.isEligibleForFullBenefits())

3. Clarify obscure argument or return value into much more readable format.

        public void testCompareTo() throws Exception {
           …
           assertTrue(a.compareTo(a) == 0);  	// a == a 
           assertTrue(a.compareTo(b) != 0);  	// a != b
           assertTrue(ab.compareTo(ab) == 0); 	// ab == ab
           assertTrue(a.compareTo(b) == -1); 	// a < b
           assertTrue(aa.compareTo(ab) == -1);  	// aa < ab
           assertTrue(ba.compareTo(bb) == -1); 	// ba < bb
           assertTrue(b.compareTo(a) == 1);  	// b > a
           assertTrue(ab.compareTo(aa) == 1); 	// ab > aa 
           assertTrue(bb.compareTo(ba) == 1); 	// bb > ba
           …
        }


4. Do not add noise comments

        /** The day of the month. */
        private int dayOfMonth;

        /**
        * Returns the day of the month. *
        * @return the day of the month. */
        public int getDayOfMonth() { 
        	return dayOfMonth;
        }

5. Add *TODO*, *FIXME* comments for the job that should be done, but for some reason do not have time to do it.

6. Do not express your emotions in comment, talk to your supervisor.

        try {
          response.add(ErrorResponder.makeExceptionString(e));
          response.closeAll(); 
        }
        catch(Exception exception) 
        {
			//Give me a break!
        }



7. Follow comment conventions. Depending on language you are using, follow common comment conventions. 

        /**
         * Return lateral location of the specified position.
         * If the position is unset, NaN is returned.
         *
         * @param x    X coordinate of position.
         * @param y    Y coordinate of position.
         * @return     Lateral location.
         * @throws IllegalArgumentException  If zone is <= 0.
         */
        public double computeLocation(double x, double y)
          throws IllegalArgumentException
        {
          ...
        }

Many programming languages do use same comment style, however for details you can refer to Java Code Conventions, for Python please refer to Python-PEP-257-Docstring Conventions.




##4.Testing


1. Test code must follow the same code conventions and programming styles.

2. Unit tests should be fully automated and non-interactive

3. Tests should be independent of each other.

4. Tests should be repeatable

5. Fix failing tests immediately and do not commit/push your code to the repository if your test is failing 

6. The person who broke the test sis responsible to fix the test without deleting the test



-----




## Inspired by

* [Java Programming Style Guidelines](http://geosoft.no/development/javastyle.html)
* Martin, R. C. (2009). Clean code: A handbook of agile software craftsmanship. Upper Saddle River, NJ: Prentice Hall.
* [Oracle (1997). Java Code Conventions](http://www.oracle.com/technetwork/java/codeconv-138413.html)
* [The Principles of OOD](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod)
* [Oracle (1997). Java Code Conventions](http://www.oracle.com/technetwork/java/codeconv-138413.html)
* [Geotechnical Software Services (2011). Unit Testing Guidelines.](http://geosoft.no/development/unittesting.html)
* [Goodger, D., Rossum, G. (2009). Docstring Conventions.](http://www.python.org/dev/peps/pep-0257/)




[ref-1]:https://docs.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/edit?pli=1

[ref-2]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/edit?hl=en&pli=1

[ref-3]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh/edit?hl=en&pli=1

[ref-4]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/edit?hl=en&pli=1

[ref-5]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgMjdlMWIzNGUtZTQ0NC00ZjQ5LTkwYzQtZjRhMDRlNTQ3ZGMz/edit?hl=en&pli=1

[ref-6]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgOGM2ZGFhNmYtNmE4ZS00OGY5LWFkZTYtMjE0ZGNjODQ0MjEx/edit?hl=en&pli=1


[ref-7]:https://docs.google.com/a/cleancoder.com/file/d/0BwhCYaYDn8EgZjI3OTU4ZTAtYmM4Mi00MWMyLTgxN2YtMzk5YTY1NTViNTBh/edit?hl=en&pli=1
