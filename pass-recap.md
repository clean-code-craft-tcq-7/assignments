# Recap of passing code

[Alignment test example](https://github.com/clean-code-craft-tcq-7/test-failer-in-py-KarthikeyaniShanmugam/blob/92347a9f0c5f7efbed82e4d6ce574a4bc98f0196/misaligned.py)

[Test as documentation](https://github.com/clean-code-craft-tcq-m-2/test-failer-in-c-DanOrta/blob/27253237b7a08eedf5fb1db377a5b675d264ef36/misaligned-test.c)

[Use of function objects in C++ for dependency injection](https://github.com/clean-code-craft-tcq-m-2/test-failer-in-cpp-RicardoGuD/blob/f966aa113272f9fca80bceeedbaa98a96e068535/alerterTest.cpp)

[Off-the-shelf functionality for alignment](https://github.com/clean-code-craft-tcq-m-2/test-failer-in-py-JorgeRuizMtz/blob/251dffae203ee948b11cca2941048515f9b7fdb5/misaligned_fixed%26Test.py)

---

Map tests to real life. Do you think a person with a 42-cm shoulder should get a t-shirt of 'invalid' size?

```java
	public static void main(String args[]) {
		assert (Tshirts.size(37) == "S");
		assert (Tshirts.size(38) == "INVALID");
		assert (Tshirts.size(40) == "M");
		assert (Tshirts.size(42) == "INVALID");
		assert (Tshirts.size(43) == "L");
		System.out.println("All is well (maybe!)");
	}
}
```

---

Testing and running different code...

```cpp
int i = 0, j = 0;
for(i = 0; i < 5; i++) {
    for(j = 0; j < 5; j++) {
        std::cout << std::left << std::setw(MAX_WIDTH) <<i * 5 + j + 1 << " | " << std::setw(MAX_WIDTH)
        << majorColor[i] << " | " << std::setw(MAX_WIDTH)<< minorColor[j] << "\n";
        
        int PairNum = ColorNum_To_PairNum(i, j, numberOfMinorColors);

        assert(PairNum == i * 5 + j + 1 ); // add 1 to get the correct
```

Is this the minimum code that can pass your tests?

```cpp
char size(int cms) {
    char sizeName = '\0';
    if(cms <= 38) {
        sizeName = 'S';
    } else if(cms > 38 && cms <= 42) {
        sizeName = 'M';
    } else if(cms > 42) {
        sizeName = 'L';
    }
    return sizeName;
}
```

Being sensitive to naming - [even in the workflow](https://github.com/clean-code-craft-tcq-4/test-failer-in-py-nisharai1/pull/1/files)

[Separation of tests, data, and code](https://github.com/clean-code-craft-tcq-4/test-failer-in-cpp-POOJASHREE-G/blob/af438c3d04230366637ba0b7deb8387ea688510d/.github/workflows/main-workflow.yml)

[Testing the parts](https://github.com/clean-code-craft-tcq-4/test-failer-in-cpp-ankit-88/blob/3970b8d1eabfbb3d6e9aca3c3e13fcf37b5c91bb/test_alerter.cpp)

[Testing exceptions](https://github.com/clean-code-craft-tcq-4/test-failer-in-py-VishnuJin/blob/c2c53b0d687bb1f0656dabd826c771841b1418c6/misaligned.py)

