Android Activity “launchMode” Explained , Must know for Android Development.
What happens , when we add this launchMode tag in an activity of Android application.
<activity android:name=”.MainActivity”
 android:launchMode=”singleTop”></activity>
Assume A , B , C , D , E , F are the Activities
launchMode=”singleTop”
We are adding launchMode=”singleTop” in D.
Example one:
Previous State of Activity Stack
D -D is on top of Activity Stack
C
B
A
Start D from any service or other application or from somewhere.

Final State of Activity Stack
D -old instance gets extras data through onNewIntent(Intent intent);
C
B
A
Example Two:
Previous State of Activity Stack
C
B
A
Start D from any service or other application or from somewhere.
Final State of Activity Stack
D -starts as usual.
C
B
A


Example Three:
Previous State of Activity Stack
C
D
B
A
Start D from C
Final State of Activity Stack
D -old instance gets extras data through onNewIntent(Intent intent);
C
B
A

launchMode=”singleTask”
We are adding launchMode=”singleTask” in C.
Example one:
Previous State of Activity Stack
D
C
B
A
Start C
Final State of Activity Stack
C -old instance gets extras data through onNewIntent(Intent intent);
B
A
info - D gets destroyed
Example Two:
Previous State of Activity Stack
B
A
Start C
Final State of Activity Stack
C -starts as usual.
B
A
launchMode=”singleInstance”
We are adding launchMode=”singleInstance” in E.
Example one:
Previous State of Activity Stack
D
C
B
A
Start E
Final State of Activity Stack
E
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — —
D
C
B
A
info — A , B , C , D will be in one task and E will be in another task.
and if we continue this , and start F from E,then
Final State of Activity Stack
F
D
C
B
A
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — -
E
info — A , B , C , D , F will be in one task and E will be in another task.
Another Example
Previous State of Activity Stack
A
B
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — -
E
Start E from A
Final State of Activity Stack
E -old instance gets extras data through onNewIntent(Intent intent);
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — — —
A
B

launchMode=”standard”
We are adding launchMode=”standard” in B.
Previous State of Activity Stack
D
C
B
A
Start B
Final State of Activity Stack
B -new instance of B
D
C
B
A
Now when we set flag programmatically:
FLAG_NEW_TASK
We are starting E from D with flag
Example one:
Previous State of Activity Stack
D
C
B
A
Final State of Activity Stack
E
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — —
D
C
B
A
info — A , B , C , D will be in one task and E will be in another task
Example Two:
We are starting B from D with flag
Previous State of Activity Stack
D
C
B
A
Final State of Activity Stack
B
— — — — — — — — — — — — — — — — — — — — — — — — — — — — — —
D
C
B
A
info — A , B , C , D will be in one task and and another B will be in another task
FLAG_CLEAR_TASK
It works in conjugation with FLAG_NEW_TASK
Example One:
We are starting E from D with flag
Previous State of Activity Stack
D
C
B
A
Final State of Activity Stack
E
info -All others will get destroyed
Example Two:
We are starting B from D with flag
Previous State of Activity Stack
D
C
B
A
Final State of Activity Stack
B -new instance of B will be created it will start as usual.
info -All others will get destroyed
FLAG_SINGLE_TOP
FLAG_SINGLE_TOP is similar to launchMode=”singleTop”
FLAG_CLEAR_TOP
We are starting B from D with flag
Previous State of Activity Stack
D
C
B
A
Final State of Activity Stack
B -old instance gets extras data through onNewIntent(Intent intent);
A
info -All others will get destroyed

