# Collapsing ToolBar/Appbar

Collapsing Appbar is another kind of **ActionBar** which can be collapsed on simple scroll. To create a collapsable AppBar we need to create a **AppBarLayout** with **CollapsingToolbarLayout** and **NestedScrollView** as children in it.

Now as it is a Toolbar we need to wrap **Toolbar** in **CollapsingToolbarLayout**.



```xml
    <com.google.android.material.appbar.AppBarLayout
        android:id="@+id/appBarLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/ThemeOverlay.AppCompat.DayNight.ActionBar">

        <com.google.android.material.appbar.CollapsingToolbarLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:layout_scrollFlags="scroll|snap|exitUntilCollapsed"
            app:contentScrim="@color/purple_200"
            app:title="@string/log_in"
            app:expandedTitleGravity="right|bottom"
            app:expandedTitleTextColor="@color/white"
            >

            <ImageView
                android:layout_width="match_parent"
                android:layout_height="250dp"
                android:src="@drawable/login"
                android:scaleType="centerCrop"
                />

            <androidx.appcompat.widget.Toolbar
                android:layout_width="match_parent"
                android:layout_height="?attr/actionBarSize"
                app:popupTheme="@style/ThemeOverlay.AppCompat.DayNight"/>

        </com.google.android.material.appbar.CollapsingToolbarLayout>

    </com.google.android.material.appbar.AppBarLayout>

    <androidx.core.widget.NestedScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior"
        >

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <com.google.android.material.textfield.TextInputLayout
                android:id="@+id/userNameWrapper"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="30dp"
                android:layout_marginTop="65dp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent">

                <com.google.android.material.textfield.TextInputEditText
                    android:id="@+id/userName"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:hint="@string/enter_username"
                    android:inputType="textEmailAddress"
                    android:maxEms="10"
                    android:minEms="6" />

            </com.google.android.material.textfield.TextInputLayout>

            <com.google.android.material.textfield.TextInputLayout
                android:id="@+id/passwordWrapper"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginTop="20dp"
                app:endIconMode="password_toggle"
                app:layout_constraintEnd_toEndOf="@id/userNameWrapper"
                app:layout_constraintStart_toStartOf="@id/userNameWrapper"
                app:layout_constraintTop_toBottomOf="@id/userNameWrapper">

                <com.google.android.material.textfield.TextInputEditText
                    android:id="@+id/password"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:hint="@string/enter_password"
                    android:inputType="textPassword"
                    android:maxEms="12"
                    android:minEms="8" />

            </com.google.android.material.textfield.TextInputLayout>

            <Button
                android:id="@+id/signUp"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="30dp"
                android:text="@string/sign_up"
                app:layout_constraintStart_toStartOf="@id/passwordWrapper"
                app:layout_constraintTop_toBottomOf="@id/passwordWrapper" />

            <Button
                android:id="@+id/signIn"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/sign_in"
                app:layout_constraintEnd_toEndOf="@id/passwordWrapper"
                app:layout_constraintTop_toTopOf="@id/signUp" />

            <TextView
                android:id="@+id/forgot"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="50dp"
                android:text="@string/forgot_password"
                android:textSize="22sp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.75"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@id/signUp" />

            <ProgressBar
                android:id="@+id/progressBar"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:visibility="invisible"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.core.widget.NestedScrollView>
```



