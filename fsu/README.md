# Florida State University (FSU) Data

## */raw/reports*

The complete dataset of course evaluation reports.

- **Source:** https://fsu.evaluationkit.com/Report/Public
- **Timeframe:** Fall 2013 - Spring 2023 (Fall, Spring, and Summer terms)

### Notes
- File names represent the search term used to gather the data, matching the first 4 characters of the course code
- Data from courses with multiple codes is almost certainly duplicated in each matching file

### Format
Files contain a serialized JSON representation of a `List<Report>`. The `Report` structure is:

```kotlin
data class Report(
  /**
   * The instructor name parsed from the pdf report.
   *
   * Note that this may contain incorrect values, like "SEE MORE ON LAST PAGE" or "SECTIONS)" before the actual name.
   *
   * "Report-ERROR" represents a broken (inaccessible) pdf.
   */
  val pdfInstructor: String,
  /** The instructor name as it appears in the html search results. Formatted as "Last, First". */
  val htmlInstructor: String,
  /** The term as it appears in the html search results. Formatted as "2023 Spring". */
  val term: String,
  /**
   * The course code as it appears in the html search results.
   *
   * Includes section numbers, and may contain several codes combined by slashes.
   */
  val courseCode: String,
  /** The course name as it appears in the html search results. */
  val courseName: String,
  /** The area as it appears in the html search results. */
  val area: String,
  /** The number of respondents as parsed from the pdf report. May be -1. */
  val numRespondents: Int,
  /**
   * The ratings, gathered from the pdf report.
   *
   * Keys are question numbers from [QuestionMapping], values are # of ratings 5-1 (# of 5s, # of 4s, ...).
   */
  val ratings: Map<Int, List<Int>>,
  /**
   * The ids present in the html search results, used for getting the pdf report url. Should have a length of 4.
   */
  val ids: List<String>,
)
val QuestionMapping = listOf(
  "The course materials helped me understand the subject matter.",
  "The work required of me was appropriate based on course objectives.",
  "The tests, project, etc. accurately measured what I learned in this course.",
  "This course encouraged me to think critically.",
  "I learned a great deal in this course.",
  "Instructor(s) provided clear expectations for the course.",
  "Instructor(s) communicated effectively.",
  "Instructor(s) stimulated my interest in the subject matter.",
  "Instructor(s) provided helpful feedback on my work.",
  "Instructor(s) demonstrated respect for students.",
  "Instructor(s) demonstrated mastery of the subject matter.",
  "Overall course content rating.",
  "Overall rating for Instructor(s)",
  "What is your year in school?",
  "What is your cumulative GPA?",
  "What grade do you expect to receive in this course?",
  "Is this a required course for you?",
).withIndex().associate { it.value to it.index }
```

## */generated*

Backend data for [EVALS: FSU](https://opletter.github.io/course-evals/fsu/).

### */stats-by-prof* 

**Source:** */raw/reports*

Excludes data from questions 0, 3, 4, and 11-16.

### */core/course-names*

**Source:** https://registrar.fsu.edu/class_search, https://flscns.fldoe.org/PbCourseDescriptions.aspx

### */core/teaching-[semester]*

**Source:** https://registrar.fsu.edu/class_search/

### */core/dept-names.json*

**Source:** https://registrar.fsu.edu/bulletin/undergraduate/information/course_prefix/

---

**Source code for the creation of this dataset is available [here](https://github.com/opLetter/course-evals/tree/master/colleges/fsu/src/main/kotlin/io/github/opletter/courseevals/fsu).**