# Threads

## AsyncTask

This method is now deprecated but still used in many projects so it is good to have an idea about it.

1. Create a class extending `AsyncTask`.
2. There are 2 main functions which we can override `doInBackground` and `onProgressUpdate` but `onPreExecute` and `onPostExecute` are also useful methods.
3. `doInbackground` method is the main method which is used to do the task intended.
4. `onProgressUpdate` method is mainly used for updating the progressBar or showing percentage of task done.
5. While creating class there are 3 paramenter which we need to pass in the `AsyncTask`.
6. 1st paramter is for the input type to `doInBackground` method, 2nd parameter is for the input type for `onProgressUpdate` method and 3rd type is used as return type of `doInBackground` method.
7. To execute the task we need to create an instance of class executing `AsyncTask` and call execute on that.

```java
// Parameter 1: parameter for doInBackground method.
// Parameter 2: parameter for onProgressUpdate method.
// Parameter 3: parameter for return type of doInBackground
private class InsertAsync extends AsyncTask<Note, Void, Void> {
    private NotesDAO notesDAO;
    InsertAsync(NotesDAO notesDAO){
        this.notesDAO = notesDAO;
    }
    // Do the task intended in doInBackground method
    @Override
    protected Void doInBackground(Note... notes) {
        notesDAO.insert(notes[0]);
        return null;
    }
}

// Somewhere in the Activity
InsertAsync(notesDao).execute();
```



## Doing same with Executor class

This is very efficient and simple way to achieve threads in android.

1. Create an ExecutorService with `Executors.newSingleThreadExecutor()`
2. To run a task inside new thread simply use `executor.execute(Runnable runnable)`
3. Define task to be executed in `run` method of Runnable.

```java
// Create a variable for ExecutorService.
ExecutorService executorService = Executors.newSingleThreadExecutor();

executorService.execute(new Runnable() {
    @Override
    public void run() {
        notesDAO.insert(note);
    }
});
```



