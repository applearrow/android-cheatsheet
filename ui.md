# Ui techs
## View Binding [:robot:](https://developer.android.com/topic/libraries/view-binding)

- module-level `build.gradle`:

```groovy
android {
    ...
    buildFeatures {
        viewBinding true
    }
}
```

- Use in a fragment

  ```kotlin
  private var _binding: ResultProfileBinding? = null
  // This property is only valid between onCreateView and
  // onDestroyView.
  private val binding get() = _binding!!
  
  override fun onCreateView(
      inflater: LayoutInflater,
      container: ViewGroup?,
      savedInstanceState: Bundle?
  ): View? {
      _binding = ResultProfileBinding.inflate(inflater, container, false)
      val view = binding.root
      return view
  }
  
  override fun onDestroyView() {
      super.onDestroyView()
      _binding = null
  }
  ```

```kotlin
binding.name.text = viewModel.name
binding.button.setOnClickListener { viewModel.userClicked() }
```

## Data Binding [:robot:](https://developer.android.com/topic/libraries/data-binding)

- module-level `build.gradle`:

  ```groovy
  android {
      ...
      buildFeatures {
          dataBinding true
      }
  }
  ```

- Enclose your layouts:

  ```xml
  <layout xmlns:android="http://schemas.android.com/apk/res/android"
          xmlns:app="http://schemas.android.com/apk/res-auto">
      <data>
          <variable
              name="viewmodel"
              type="com.myapp.data.ViewModel" />
      </data>
      <ConstraintLayout... /> <!-- UI layout's root element -->
  </layout>
  ```

  | layout            | Class generated     |
  | ----------------- | ------------------- |
  | activity_main.xml | ActivityMainBinding |

  

- Use in an activity

  ```kotlin
  override fun onCreate(savedInstanceState: Bundle?) {
      super.onCreate(savedInstanceState)
  
      val binding: ActivityMainBinding = DataBindingUtil.setContentView(
              this, R.layout.activity_main)
  
      binding.user = User("Test", "User")
  }
  ```

## Jetpack Compose [:robot:](https://developer.android.com/jetpack/compose)
