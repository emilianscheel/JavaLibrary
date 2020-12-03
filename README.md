# Java Library

## android java code examples
* [Retrieving Firebase Data list into an recyclerview](#Retrieving-Firebase-Data-in-Recyclerview)

## Retrieving-Firebase-data-in-Recyclerview
This is for showing Firebase Realtime data in an android recyclerview.

### 1. Connect your Firebase with your app 
In Android Studio go to top menu bar to "Tools > Firebase". In the right site bar click "Realtime Database" and "Connect" it with your online Firebase account.

### 2. Create user list example in Firebase

![here_should_be_the_example](https://github.com/emilianscheel/android-java-library/blob/main/firebase-user-list-example.png)

### 3. Copy this into your android application
```
ArrayList<UserItem> mList = new ArrayList<>();
DatabaseReference databaseReference = FirebaseDatabase.getInstance().getReference("user");
RecylerView recyclerView = findViewById(R.id.recyclerview);

recyclerView.setHasFixed(true);
recyclerView.setLayoutManager(new LinearLayoutManager(this));

databaseReference.addValueEventListener(new ValueEventListener() {
    @Override
    public void onDataChange(@NonNull DataSnapshot snapshot) {

        if (snapshot.hasChildren()) {

            for (DataSnapshot dataSnapshot : snapshot.getChildren()) {

                final UserItem user = dataSnapshot.getValue(UserItem.class);
                mList.add(user);
            }

        Adapter adapter = new Adapter(mList);
        recyclerView.setAdapter(adapter);
        adapter.notifyDataSetChanged();
        }
    }

    @Override
    public void onCancelled(@NonNull DatabaseError error) {

    }
});
```

### 4. Also copy the "Adapter Class" and "Item Class"
Required is 
* a empty "Constructor" and a full "Constructor"
* Getter and Setter for every String, Integer, Long, ...
```

public class UserItem {

    String user_name;
    String user_id;
    
    String joined_day;
    String joined_month;
    String joined_year;

    public UserItem(String user_name, String user_id, String joined_day, String joined_month, String joined_year) {
        this.user_name = user_name;
        this.user_id = user_id;
        this.joined_day = joined_day;
        this.joined_month = joined_month;
        this.joined_year = joined_year;
    }
    
    public String getUser_name() {
        return user_name;
    }

    public void setUser_name(String user_name) {
        this.user_name = user_name;
    }
    
    public String getUser_id() {
        return user_name;
    }

    public void setUser_id(String user_id) {
        this.user_id = user_id;
    }
    
    public String getJoined_day() {
        return joined_day;
    }

    public void setJoined_day(String joined_day) {
        this.joined_day = joined_day;
    }
    
    public String getJoined_month() {
        return joined_month;
    }

    public void setJoined_month(String joined_month) {
        this.joined_month = joined_month;
    }
    
    public String getJoined_year() {
        return joined_year;
    }

    public void setJoined_year(String joined_year) {
        this.joined_year = joined_year;
    }
    
}

```

