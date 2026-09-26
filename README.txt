QUESTIONNAIRE WITH EDITABLE WORD BANKS

FILES
index.html: Updated version of your questionnaire.
practice_pairs.txt: All 3 original mock/practice pairs.
actual_test_pairs.txt: All 52 original main-test pairs.

USING THE FILES
Keep these three files together in the same folder. Upload all three to the
same folder on your study's web host, then visit index.html.
For local testing, open a terminal in that folder and run:
python3 -m http.server 8000
Then visit http://localhost:8000 in your browser.
Opening index.html by double-clicking will not load the text files.
The existing jsPsych library links require an internet connection.

EDITING THE TEXT FILES
The .txt files contain JSON. Edit them in a plain-text editor and save as UTF-8.
Each object in the array represents one pair. Use these exact field names:
pair_id: A unique identifier within that file. Preserve existing IDs when
         changing wording for the same item. Practice IDs are strings such as
         "P1"; the provided main IDs are numbers such as 1.
word1: First adjective in the canonical data record.
word2: Second adjective in the canonical data record.
condition: "practice" in the practice file. In the main file, use
           "matched_positive", "matched_negative", or "mixed".
more_desirable: For "mixed", exactly match word1 or word2, including case.
                For the other conditions, leave it as "".

Example of a main-test entry:
{
  "pair_id": 27,
  "word1": "Agreeable",
  "word2": "Tense",
  "condition": "mixed",
  "more_desirable": "Agreeable"
}

Keep double quotes around field names and text values. Separate objects with
commas, but do not put a comma after the final object. Keep the outer [ and ].
Do not add comments inside JSON. Reload the page after editing.

WHAT CHANGED
The two embedded word-bank arrays were moved into separate files.
startStudy() waits for both files to load and pass validation before building
the timeline. Invalid files produce a visible startup error.
The displayed practice and main pair counts now follow the loaded data.
Words are escaped before insertion into HTML so they appear as literal text.
Practice order, main-trial shuffling, randomized left/right sides, S/K keys,
500 ms fixation, and existing response/Qualtrics handling are preserved.
As in your original code, only mixed main pairs receive a desirability score;
practice responses are not included in the final Qualtrics trial payload.
The text files define stimuli, not a place to save participant responses.

VALIDATION SCOPE
The supplied data and timeline/scoring logic were checked programmatically.
A full participant run and the external Qualtrics handoff still need to be
verified in your study hosting environment before collecting responses.
