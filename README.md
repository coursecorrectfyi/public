# Update Course Reviews and Ratings

We have course data from various online course providers like Skillshare, Udemy, Coursera, edX, etc.
<details>
<summary>The Course Object (simplified)</summary>

```json5
{
    "_id" : "6655a4844a5f49e2ea1018d5",
    "properties" : {
        "course_name" : "Short Films 101: Plan, Capture, and Edit Cinematic Shorts",
        "course_provider" : "Skillshare",
        "course_num_rating" : 0,
        "course_avg_rating" : 0,
        "course_is_free" : false
    },
    "courseUrl" : "https://www.skillshare.com/en/classes/short-films-101-plan-capture-and-edit-cinematic-shorts/1129254486"
}
```
</details>

We also have reviews for these courses in a separate collection.
<details>
<summary>The CourseReview Object</summary>

```json5
{
    "_id" : "6680ea5cd82b560fad8a173a",
    "courseId" : "6655a4844a5f49e2ea1018d5",
    "title" : "(reviewer name)",
    "review_stars" : "Five out of five stars",
    "datetime" : "2023-06-22",
    "review" : "(the view text)"
}
```
</details>

## What We Need

- For each of these courses, we need to 
  - replace our existing reviews with the 20 most recent reviews from the original course page (`course.courseUrl`)
  - replace the `courses.properties.course_num_rating` with the total number of reviews for the course, from the original course page
  - replace the `courses.properties.course_avg_rating` with the average rating (a decimal number from 1 to 5), from the original course page
- Verify that this is reflected on the portal

### Additional Factors
- It’s possible that some courses don’t exist anymore. In such cases
  - Backup that course in a separate mongo collection (`deleted_courses`)
  - Delete	that course from our original collection
- Consider possible failures in the process and their handling
- This is the priority of course providers for us
  - Coursera
  - Pluralsight
  - edX
  - Skillshare
  - DataCamp
  - YouTube
  - Udemy
  - LinkedIn Learning
