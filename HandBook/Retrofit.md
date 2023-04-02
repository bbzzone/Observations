# Retrofit

Retrofit is a library which can be used to make api calls for the android application. Other alternative for retrofit is volley. Retrofit turns the api calls to a `Java Interaface` 



1. Create an object of `Retrofit` using builder.

   1. ```java
      // base url is the url from where to fetch the data.
      Retrofit retrofit = new Retrofit.Builder().baseUrl("https://jsonplaceholder.typicode.com/")
                      .addConverterFactory(GsonConverterFactory.create())
                      .build();
      ```

2. Create a class which will be used to store the data received from the api call. Variables should be nameed as the key of the value which will be received from api calls, otherwise one has to specify the name using `@SerializedName("body")` annotation.

   1. ```java
      // assume api call returns an json object with following
      // keys {userId, id, title, body}
      public class ModelClass {
          private int userId;
          private int id;
          private String title;
          
          // as object we are receiving has key 
          // named "body" we have to specify it
          // if the variable name is other than that.
          @SerializedName("body")
          private String subTitle;
      
          public int getUserId() {
              return userId;
          }
      
          public int getId() {
              return id;
          }
      
          public String getTitle() {
              return title;
          }
      
          public String getSubTitle() {
              return subTitle;
          }
      }
      ```

3. Create an interface which will have an object of type `Call<List<ModelClass>>`.  And annotate it with `GET` and pass the relative URL of the source. Every method in this interface should be annotated with its type i.e. `POST, GET, PUT, PATCH, DELETE, HEAD, HTTP, OPTIONS`.

   1. ```java
      public interface RetrofitAPI {
          @GET("posts")
          Call<List<ModelClass>> getModelClass();
      }  
      ```

4. Now create an instance of Interface created in previous step using `RetrofitAPI service = retrofit.create(RetrofitAPI.class);`. 

5. Create an instance of `Call<List<ModelClass>` and call enque on object where we can handle request results.

   1. ```java
      Call<List<ModelClass>> call = service.getModelClass();
      
      call.enqueue(new Callback<List<ModelClass>>() {
          @Override
          public void onResponse(
              Call<List<ModelClass>> call, 
              Response<List<ModelClass>> response) 
          {
              if (!response.isSuccessful()) {
                  Toast.makeText(MainActivity.this, "No Response", Toast.LENGTH_SHORT).show();
              } else {
                  List<ModelClass> resp = response.body();
                  adapter = new RecyclerAdapter(resp);
                  binding.recycler.setAdapter(adapter);
              }
          }
      
          @Override
          public void onFailure(Call<List<ModelClass>> call, Throwable t) {
              Toast.makeText(MainActivity.this, "An Error Occurred", Toast.LENGTH_SHORT).show();
          }
      });
      ```

   2. We can get the data using `data.get(position).getUserId()` in recycler adapter. **(data is the resp object passed to the recycler adpater)**.

    