
### params -
```js
import { useParams } from "react-router";
function EditContact() {
const { id } = useParams();

}
```


---

### Basic structure (of jsx) -
State
handleChange
Form
Inputs
Buttons


---

### React conventions -
onClick

onSubmit

onChange

onDelete (custom)

onSave (custom)

onEdit (custom)


---

### Functional State Update -
Jab nayi state

**purani state pe depend karti hai**

Tab

```
setState(previous=>...)
```
```js
    setFormData((previousFormData) => ({

      ...previousFormData,

      [name]: value,

    }));
// Ye guaranteed latest state use karega.
  }
```