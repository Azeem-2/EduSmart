# EduSmart Schema 

Learning Resource:

https://www.milowski.com/journal/entry/2024-06-26T12:00:00-07:00/


EduSmartSchema declared via phrases:

```gql
CREATE GRAPH TYPE EduSmartSchema AS {

   -- Node Definitions

   NODE :Program {
      name :: STRING NOT NULL,
      description :: STRING
   },

   NODE :Course {
      course_number :: STRING NOT NULL,
      name :: STRING NOT NULL,
      description :: STRING
   },

   NODE :Class {
      section_number :: STRING NOT NULL,
      start_date :: DATE NOT NULL,
      end_date :: DATE NOT NULL,
      class_days_of_week :: STRING NOT NULL,
      class_time :: TIME NOT NULL,
      class_duration :: DURATION NOT NULL,
      lab_days_of_week :: STRING NOT NULL,
      lab_time :: TIME NOT NULL,
      lab_duration :: DURATION NOT NULL
   },

   NODE :Person {
      name :: STRING NOT NULL,
      url :: STRING,
      givenName :: STRING,
      familyName :: STRING NOT NULL,
      birthDate :: DATE NOT NULL,
      signupDate :: DATETIME NOT NULL
   },

   NODE :Student => :Person {
      student_id :: STRING NOT NULL
   } AS Student,

   NODE :Teacher => :Person {
      teacher_id :: STRING NOT NULL
   } AS Teacher,

   NODE :TextBook {
      title :: STRING NOT NULL,
      author_name :: STRING NOT NULL,
      description :: STRING
   },

   NODE :Topic {
      title :: STRING NOT NULL,
      url :: STRING,
      details :: STRING,
      lastReviewed :: STRING NOT NULL,
      creationDate :: DATE NOT NULL,
      sequenceNumber :: INT NOT NULL
   },

   NODE :Interaction {
      title :: STRING NOT NULL,
      author_name :: STRING NOT NULL,
      description :: STRING
   },

   -- Edge Definitions

   DIRECTED EDGE contains {} CONNECTING (Program -> Course),

   DIRECTED EDGE scheduled {} CONNECTING (Course -> Class),

   DIRECTED EDGE admission {} CONNECTING (Student -> Program),

   DIRECTED EDGE registers {} CONNECTING (Student -> Class),

   DIRECTED EDGE teaches {} CONNECTING (Teacher -> Class),

   DIRECTED EDGE taught {} CONNECTING (Course -> TextBook),

   DIRECTED EDGE contains {} CONNECTING (Topic -> TextBook),

   DIRECTED EDGE contains {} CONNECTING (Topic -> Topic),

   DIRECTED EDGE knows 
      { 
        level :: INT NOT NULL, 
        assessment_date :: DATETIME 
      } 
      CONNECTING (Student -> Topic),

   DIRECTED EDGE covers {} CONNECTING (Interaction -> Topic)

}

```




