1.  Create a standard regional bucket with your closest region with a globally unique name.

    >     gsutil mb -l (YOUR_REGION) gs://(BUCKET_NAME)

2.  Enable versioning for the bucket.

    >     gsutil versioning set on gs://(BUCKET_NAME)

3.  In your Cloud Shell session, create a text file called ‘file.txt’. In the file, add the text ‘version 1’, then save the changes.

    >     vim file.txt
    > 
    > Hit 'I' to Insert, type 'version 1', ESC key, :wq

4.  Copy ‘file.txt’ to your bucket.
    
    >     gsutil cp file.txt gs://(BUCKET_NAME)

5.  Edit the ‘file.txt’ in Cloud Shell to say ‘version 2’ instead of ‘version 1’, then save the change.

    > `vim file.txt`
    > 
    > Hit 'I' to Insert, type 'version 2' in place of 'version 1', ESC key, :wq

6.  Copy ‘file.txt’ to your bucket again.

    >     gsutil cp file.txt gs://(BUCKET_NAME)

7.  Edit the ‘file.txt’ in Cloud Shell to say ‘version 3’ instead of ‘version 2’, then save the change.

    > `vim file.txt`
    > 
    > Hit 'I' to Insert, type 'version 3' in place of 'version 2', ESC key, :wq

8.  Copy ‘file.txt’ to your bucket one more time.
    
    >     gsutil cp file.txt gs://(BUCKET_NAME)

9.  Delete ‘file.txt’ from Cloud Shell.

    >     rm file.txt

10.  List the contents of your bucket.

    >     gsutil ls gs://(BUCKET_NAME)

11.  List the contents of your bucket again, but show all versions of your document.

    >     gsutil ls -a gs://(BUCKET_NAME)

12.  Copy ‘file.txt’ from your bucket to Cloud Shell without specifying a generation number. View the contents of the file, what text do you have in the ‘version \[X\]’ line?

    >     gsutil cp gs://(BUCKET_NAME)/file.txt .

13.  Delete ‘file.txt’ from Cloud Shell.

    >     rm file.txt

14.  Copy ‘file.txt’ from your bucket to Cloud Shell, this time specifying the highest generation number. View the contents of the file, what text do you have in the ‘version \[X\]’ line?

    >     gsutil cp gs://(BUCKET_NAME)/file.txt#(HIGHEST_GENERATION) .

15.  Delete ‘file.txt’ from Cloud Shell.

    >     rm file.txt

16.  Copy ‘file.txt’ from your bucket to Cloud Shell specifying the lowest generation number. View the contents of the file, what text do you have in the ‘version \[X\]’ line?

    >     gsutil cp gs://(BUCKET_NAME)/file.txt#(LOWEST_GENERATION) .

17.  Delete ‘file.txt’ from Cloud Shell.

    >     rm file.txt

18.  Delete ‘file.txt’ from your bucket.

    >     gsutil rm gs://(BUCKET_NAME)/file.txt

19.  From your web console, view the contents of your bucket. Is there anything there?

    > View Cloud Storage Browser in the web console.

20.  From Cloud Shell list contents of your bucket. Is there anything there?

    > gsutil ls gs://(BUCKET\_NAME)

21.  From Cloud Shell list contents of your bucket again, but use the option to view details/versions. Is there anything there now?

    >     gsutil ls -a gs://(BUCKET_NAME)

22.  Restore the oldest version of your ‘file.txt’ file in the bucket as the live version. It will be the one with the lowest generation number.

    >     gsutil cp gs://(BUCKET_NAME)/file.txt#(LOWEST_GENERATION_NUMBER) gs://(BUCKET_NAME)/file.txt

23.  From your web console, view the contents of your bucket. Click the ‘file.txt’ file to open it and observe which version text is in the document.

24.   Delete ‘file.txt’ from Cloud Shell and delete ALL versions of ‘file.txt’ from your bucket.

    >     gsutil rm -r gs://(BUCKET_NAME)/file.txt

25.  From Cloud Shell list contents of your bucket one last time and use the option to view details/versions. Is there anything there now? There should not be as we recursively deleted all versions.

    >     gsutil ls -a gs://(BUCKET_NAME)