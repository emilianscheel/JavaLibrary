# Java Library

## android java code examples
* [Retrieving Firebase Data list into an recyclerview](#Retrieving-Firebase-Data-in-Recyclerview)

## Retrieving-Firebase-data-in-Recyclerview
This is for showing Firebase Realtime data in an android recyclerview.

### Firebase data list example

![here_should_be_the_example](https://github.com/emilianscheel/android-java-library/blob/main/firebase-user-list-example.png)

### Retrieve this into recyclerview with 
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
