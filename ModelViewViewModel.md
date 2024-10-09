# ModelViewViewModel
ModelViewViewMode

```
class Counter {
    @JvmOverloads
    @Composable
    fun CounterScreen(viewModel: CounterViewModel = viewModel()) {
        // Collect the state from the ViewModel
        val counterValue = viewModel.counter.collectAsState()

        // UI layout
        Column(
            modifier = Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            // Display the counter value
            Text(text = "Counter: ${counterValue.value}", style = MaterialTheme.typography.headlineMedium)

            Spacer(modifier = Modifier.height(16.dp))

            // Buttons to increment and decrement the counter
            Row {
                Button(onClick = { viewModel.decrementCounter() }) {
                    Text("Decrement")
                }

                Spacer(modifier = Modifier.width(16.dp))

                Button(onClick = { viewModel.incrementCounter() }) {
                    Text("Increment")
                }
            }
        }
    }
}
````
````
class CounterViewModel : ViewModel() {

    // StateFlow to hold the counter value
    private val _counter = MutableStateFlow(0)
    val counter: StateFlow<Int> = _counter

    // Function to increment the counter
    fun incrementCounter() {
        viewModelScope.launch {
            _counter.value += 1
        }
    }

    // Function to decrement the counter
    fun decrementCounter() {
        viewModelScope.launch {
            _counter.value -= 1
        }
    }
}
````
````
class MainActivity : ComponentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            ViewModel_ModelViewTheme {

                   Counter().CounterScreen()
                }
            }
        }
    }
