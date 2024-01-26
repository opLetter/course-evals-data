# Texas State University (TXST) Data

## */raw/reports*

The complete dataset of course evaluation reports.

- **Source:** https://hb2504.txst.edu/
- **Timeframe:** Fall 2021 - Fall 2023 (Fall, Spring, and Summer terms)

### Notes
- Data is organized by instructor, with the file names corresponding to the instructor's plid
- Reports for courses with multiple instructors are duplicated in each instructor's file

### Format
Files contain a serialized JSON representation of a `List<Report>`. The `Report` structure is:

```kotlin
data class Report(
    @SerialName("class")
    val course: ReportClass,
    @SerialName("spimulti")
    val responses: List<SaveableResponse>,
)
data class ReportClass(
    /**
     * A 6-digit representation of the semester, where the last 2 digits represent the term
     * (10 = fall, 30 = spring, 50 = summer) and the first 4 digits represent the year if the term is Spring or Summer,
     * or one greater than the year if the term is Fall.
     *
     * Examples: 2021 Fall = 202210, 2022 Spring = 202230, 2022 Summer = 202250
     */
    val semester: Int,
    val title: String,
    @SerialName("student_count")
    val studentCount: Int,
    val section: String,
    val number: String,
)
data class SaveableResponse(
    val responseCount: Int,
    val instructor: TXSTInstructor,
    /**
     * The results of the survey, as a list of # of responses 1-5 (# of 1s, # of 2s, ...).
     * See [Questions] for the order of questions.
     */
    val scores: List<List<Int>>,
)
data class TXSTInstructor(
    val title: String,
    @SerialName("displayname")
    val displayName: String,
    val plid: String,
)
val Questions = listOf(
    "The instructor provided opportunity to learn",
    "The instructor communicated effectively",
    "The instructor conducted class as scheduled",
    "The course goals were made clear",
    "The course was organized effectively",
)
```

## */generated*

Backend data for [EVALS: TXST](https://opletter.github.io/course-evals/txst/).

### */stats-by-prof* 

**Source:** */raw/reports*

### */core/course-names*

**Source:** http://www.txhighereddata.org/interactive/UnivCourse/

### */core/teaching-[semester]*

**Source:** https://ssb-prod.ec.txstate.edu/PROD/bwckschd.p_get_crse_unsec

### */core/dept-names.json*

**Source:** https://ssb-prod.ec.txstate.edu/PROD/bwckgens.p_proc_term_date

---

**Source code for the creation of this dataset is available [here](https://github.com/opLetter/course-evals/tree/master/colleges/txst/src/main/kotlin/io/github/opletter/courseevals/txst).**
