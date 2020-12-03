# Java Library

## android java code examples
* [Retrieving Firebase Data list into an recyclerview](#Retrieving-Firebase-Data-in-Recyclerview)

## Retrieving-Firebase-data-in-Recyclerview
This is for showing Firebase Realtime data in an android recyclerview.

### 1. Connect your Firebase with your app 
In Android Studio go to top menu bar to "Tools > Firebase". In the right site bar click "Realtime Database" and "Connect" it with your online Firebase account.

### 2. Create Firebase user list example

![here_should_be_the_example](https://github.com/emilianscheel/android-java-library/blob/main/firebase-user-list-example.png)

### Retrieve this into recyclerview
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
