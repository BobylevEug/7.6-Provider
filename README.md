# 7.6-Provider

## 1.

<https://github.com/hashicorp/terraform-provider-aws/tree/main/aws>

```
ConflictsWith: []string{"name_prefix"},


"name": {
  Type:          schema.TypeString,
  Optional:      true,
  ForceNew:      true,
  Computed:      true,
  ConflictsWith: []string{"name_prefix"},
  ValidateFunc:  validateSQSQueueName,
},
```

менее 80 символов

```
func validateSQSQueueName(v interface{}, k string) (ws []string, errors []error) {
  value := v.(string)
  if len(value) > 80 {
     errors = append(errors, fmt.Errorf("%q cannot be longer than 80 characters", k))
  }

  if !regexp.MustCompile(`^[0-9A-Za-z-_]+(\.fifo)?$`).MatchString(value) {
     errors = append(errors, fmt.Errorf("only alphanumeric characters and hyphens allowed in %q", k))
  }
  return
}
```

```
^[0-9A-Za-z-_]+(\.fifo)?$` 
```
