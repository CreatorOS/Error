# Error

An error will undo all changes made to the state during a transaction.

You can throw an error by calling `require`, `revert` or `assert`.

## require

- `require` is used to validate inputs, conditions before execution and return values from calls to other functions.

Write this function which throws an error if the input is not greater than 10.

```
    function testRequire(uint _i) public pure {
        require(_i > 10, "Input must be greater than 10");
    }
```

Hit `Run` to test if the error is thrown or not.

## revert

- `revert` is similar to `require`.
- `revert` is useful when the condition to check is complex

This function does same thing as before:

```
    function testRevert(uint _i) public pure {
        if (_i <= 10) {
            revert("Input must be greater than 10");
        }
    }
```

Hit `Run` to test if the error is thrown or not.

## assert

- `assert` is used to check for code that should never be false. Failing assertion probably means that there is a bug.
- `assert` should only be used to test for internal errors and to check invariants.

Let's write a function to test assert:

- Here we assert that num is always equal to 0 since it is impossible to update the value of num here

```
    uint public num;

    function testAssert() public view {
        assert(num == 0);
    }
```

## Custom error

We can use custom error to save gas.

```
    error InsufficientBalance(uint balance, uint withdrawAmount);

    function testCustomError(uint _withdrawAmount) public view {
        uint bal = address(this).balance;
        if (bal < _withdrawAmount) {
            revert InsufficientBalance({balance: bal, withdrawAmount: _withdrawAmount});
        }
    }
```
