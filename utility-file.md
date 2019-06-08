


# Table of Contents
1. [Markdown](#markdown)
2. [Linux](#Linux)
3. [Maven](#Maven)


## Markdown
--------------------------------------
https://www.markdownguide.org/basic-syntax/

- Fenced Code Block	: 	

```

        ```
        {
          "firstName": "Pradeip",
          "lastName": "Patel",
          "mobile": 0000000
        }
        ```
	
```
```
- Footnote 		: 	Here's a sentence with a footnote. [^1]
					
          [^1]: This is the footnote.
			
- Heading		:	### My Great Heading {#custom-id}

- Definition List 	term

  : definition

- Strikethrough	:	~~The world is flat.~~  {without space}

- Task List		: 	- [x] Write the press release

  - [ ] Update the website
  - [ ] Contact the media 
 
 - Bold : **some text**  or  __some text__	(without space)

- Table	: 	

    | Syntax 		| Description |
    | ----------- 	| ----------- |

 
 
``` 
  
```
# Table of Contents
1. [Example](#example)
2. [Example2](#example2)
3. [Third Example](#third-example)

## Example
## Example2
## Third Example
```


## Maven

1. Create a Java Project
- mvn archetype:generate -DgroupId=com.poc.hb2co -DartifactId=HB2CO -DarchetypeArtifactId=maven-archetype-quickstart
2. build and package as a jar 		:mvn clean package
3. eclipse build			:mvn clean eclipse:eclipse

Web Project
Create a web project from Maven template maven-archetype-webapp
mvn archetype:generate 
	-DgroupId={project-packaging}
	-DartifactId={project-name}
	-DarchetypeArtifactId={maven-template} 
	-DinteractiveMode=false


## Linux

Ubuntu 



