# External (template)

Class `Napi::External<T>` inherits from class [`Napi::Value`][].

The `Napi::External` template class implements the ability to create a `Napi::Value` object with arbitrary C++ data. It is the user's responsibility to manage the memory for the arbitrary C++ data.

`Napi::External` objects can be created with an optional Finalizer function and optional Hint value. The Finalizer function, if specified, is called when your `Napi::External` object is released by Node's garbage collector. It gives your code the opportunity to free any dynamically created data. If you specify a Hint value, it is passed to your Finalizer function.

Note that `Napi::Value::IsExternal()` will return `true` for any external value.
It does not differentiate between the templated parameter `T` in
`Napi::External<T>`. It is up to the addon to ensure an `Napi::External<T>`
object holds the correct `T` when retrieving the data via
`Napi::External<T>::Data()`. One method to ensure an object is of a specific
type is through [type tags](./object.md#TypeTag).

## Methods

### New

```cpp
template <typename T>
static Napi::External Napi::External::New(napi_env env, T* data);
```

- `[in] env`: The `napi_env` environment in which to construct the `Napi::External` object.
- `[in] data`: The arbitrary C++ data to be held by the `Napi::External` object.

Returns the created `Napi::External<T>` object.

### New

```cpp
template <typename T>
static Napi::External Napi::External::New(napi_env env,
                    T* data,
                    Finalizer finalizeCallback);
```

- `[in] env`: The `napi_env` environment in which to construct the `Napi::External` object.
- `[in] data`: The arbitrary C++ data to be held by the `Napi::External` object.
- `[in] finalizeCallback`: A function called when the `Napi::External` object is released by the garbage collector accepting a T* and returning void.

Returns the created `Napi::External<T>` object.

### New

```cpp
template <typename T>
static Napi::External Napi::External::New(napi_env env,
                    T* data,
                    Finalizer finalizeCallback,
                    Hint* finalizeHint);
```

- `[in] env`: The `napi_env` environment in which to construct the `Napi::External` object.
- `[in] data`: The arbitrary C++ data to be held by the `Napi::External` object.
- `[in] finalizeCallback`: A function called when the `Napi::External` object is released by the garbage collector accepting T* and Hint* parameters and returning void.
- `[in] finalizeHint`: A hint value passed to the `finalizeCallback` function.

Returns the created `Napi::External<T>` object.

### Data

```cpp
T* Napi::External::Data() const;
```

Returns a pointer to the arbitrary C++ data held by the `Napi::External` object.

[`Napi::Value`]: ./value.md
