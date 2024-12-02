# Debugging Challenge Solution

## Corrected Code

```python
def get_service_description(service_name):
    services_map = load_services()
    sorted_keys = list(services_map.keys())
    index = sorted_keys.index(service_name)
    mapped_key = sorted_keys[(index + len(sorted_keys)) % len(sorted_keys)]  # Corrected modulo usage
    return services_map[mapped_key]
```

---

## Explanation

### Faulty Line:

```python
mapped_key = sorted_keys[(index + len(sorted_keys)) % len(service_name)]
```

- The modulo operator uses the length of `service_name` (`len(service_name)`) instead of the length of the `sorted_keys` list (`len(sorted_keys)`).
- This can cause an `IndexError` or map the service to an unrelated key.

### Corrected Line:

```python
mapped_key = sorted_keys[(index + len(sorted_keys)) % len(sorted_keys)]
```

- The modulo operator now correctly ensures that the index wraps around the length of the `sorted_keys` list.

---

### Example Behavior

#### Input

```python
get_service_description("Hackathons")
```

#### Output

- **Before Fix**:
  - Might return:
    `"Collaborate with peers for mutual growth."` (Incorrect description for "Peer Mentorship")
- **After Fix**:
  - Returns:
    `"Participate in exciting coding competitions."` (Correct description)
