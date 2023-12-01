# University of South Florida (USF) Data

## */raw/reports*

The complete dataset of course evaluation reports.

- **Source:** https://fair.usf.edu/EvaluationMart/
- **Timeframe:** Fall 2005 - Spring 2023 (Fall, Spring, and Summer terms)

### Notes
- Data is organized in directories by course prefix
- Each subdirectory contains a file for each term, named with the 4-digit year followed by a 2-digit code representing the semester (01 = Spring, 05 = Summer, 08 = Fall)

### Format
Files contain a serialized JSON representation of a `List<Report>`. The `Report` structure is:

```kotlin
data class Report(
    /** Information about the course's categorization, generally in the form "Campus - College - Department". */
    val deptInfo: String,
    /** The course's instructor, formatted as "Last, First". */
    val prof: String,
    /** The course's term, formatted as "Spring 2020". */
    val term: String,
    /** The title of the course. */
    val courseTitle: String,
    /** The course ID, formatted as "XXX - #### - ### / CRN : ######". */
    val courseID: String,
    /** The number of students enrolled in the course. */
    val enrolled: String,
    /** The number of students who responded to the evaluation. */
    val responded: String,
    /** 
     * The results of the survey, as a list of # of responses 1-5 (# of 1s, # of 2s, ...). 
     * See [Questions] for the order of questions.
     */
    val ratings: List<List<Int>>,
)
val Questions = listOf(
    "Description of Course Objectives & Assignments",
    "Communication of Ideas and Information",
    "Expression of Expectations for Performance",
    "Availability to Assist Students In or Out of Class",
    "Respect and Concern for the Students",
    "Stimulation of Interest in the Course",
    "Facilitation of Learning",
    "Overall Rating of the Instructor",
)
```

## */generated*

Backend data for [EVALS: USF](https://opletter.github.io/course-evals/usf/).

### */stats-by-prof* 

**Source:** */raw/reports*

Only based on data from Fall 2012 onwards. 

### */core/course-names*

**Source:** https://cloud.usf.edu/academic-programs/course-inventory, https://flscns.fldoe.org/PbCourseDescriptions.aspx

### */core/teaching-[semester]*

**Source:** https://usfonline.admin.usf.edu/pls/prod/bwckschd.p_disp_dyn_sched

### */core/dept-names.json*

**Source:** https://usfonline.admin.usf.edu/pls/prod/bwckschd.p_disp_dyn_sched

---

**Source code for the creation of this dataset is available [here](https://github.com/opLetter/course-evals/tree/master/colleges/usf/src/main/kotlin/io/github/opletter/courseevals/usf).**