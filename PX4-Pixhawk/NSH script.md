```shell
if [ "$PX4_SIM_MODEL" = "none" ] || [ -z $PX4_SIM_MODEL ]; then
    # some code here
fi
```

1. `[ "$PX4_SIM_MODEL" = "none" ]`: This checks if the value of the environment variable `PX4_SIM_MODEL` is equal to the string "none". The `=` operator is used for string comparison.
2. `[ -z $PX4_SIM_MODEL ]`: This checks if the value of the environment variable `PX4_SIM_MODEL` is an empty string. The `-z` test is true if the length of the string is zero.