# Reduce complexity - Recap

## Abstractions and domain

Feed an array of values and limits to [check_battery_status](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-py-Fasith/blob/66b95cb2676f58bc3ae05117207c8421bf377417/check_limits.py)

Extension with more parameters does not increase the complexity of [batteryIsOk](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-c-NabilCob/blob/5bf1296f3399d68cc5e7e42b2005a60621fbaa03/BatteryStatus.c)

[Naming functions by purpose](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-java-RaghavanVijayakumar/blob/68796261c6454b54bd2ad7dd5b620c45e5ad7311/vitals/BMSControl.java) makes the code easy to read.

[Using specific names for files](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-cs-MeenaMadhevanpillaiArunadevi) makes it easy to look for functionality. The first file you open is likely to be the right one.

---

[Avoid primitive obsession](https://refactoring.guru/smells/primitive-obsession).
This code is in the right direction:

```c
int batteryIsOk() 
{
  if(get_OutOfRange_Status() == 0)
    return E_OK;
  else
    return E_NOT_OK;
}
```

Can you think of a more domain-specific name?

---

## Name = purpose

Does `minBoundaryCheck` mean `isAboveMinimum` or `isBelowMinimum`?
Every place this function is called, a reader would need to refer to the implementation.

```c
bool minBoundaryCheck(float value,float min) {
  return !(value < min); 
}
```

---

## Complexity warning -> Concise code

Here is a code with complexity of 4. See the improvement below:

```cs
bool CheckBatteryIsOk(float temperature, float soc, float chargeRate) 
{
    bool tempOk = CheckTemperature(temperature);
    bool socOk = CheckSoc(soc);
    bool chargeRateOk = CheckChargeRate(chargeRate);

    if(tempOk && socOk && chargeRateOk == true) {
        return true;
    }
    else return false;
}
```

Complexity-prompt is an indication to write concisely

```cs
bool CheckBatteryIsOk(float temperature, float soc, float chargeRate) 
{
    bool tempOk = CheckTemperature(temperature);
    bool socOk = CheckSoc(soc);
    bool chargeRateOk = CheckChargeRate(chargeRate);

   return (tempOk && socOk && chargeRateOk);
}
```

---

Conditions nested in code: but temperature is independent of soc in real-life.
This will cause code to get 'modified' when the customer asks to 'add' the ability to give multiple independent alerts.

```c
bool ValidateTemperatureAndStateOfCharge(float temperature_data, float soc)
{            
        if (!ValidateData(temperature_data,temp_min,temp_max)) {
            return false;
        }
        else {
            if (!ValidateData(soc,soc_min,soc_max)) {
                return false;
            } else {
                return true;
            }
        }      
    }       
```

---

(From TCQ-4) Three classes or one class with parameters?

- https://github.com/clean-code-craft-tcq-4/simple-monitor-in-cpp-ankit-88/blob/714e62b76caff73c3230c8d95654fd3920dd2fdd/checker.hpp
- https://github.com/clean-code-craft-tcq-4/simple-monitor-in-py-rahulkumar082

## Extensions

[Isolating all language strings in a file](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-java-SrinathS10/blob/0d3daa75b73d6989af73c45e3d5ad9b812effcf9/BatteryMessages.txt). The fact that it's a txt file makes it easier to exchange with a translation agency.

Think of a test to ascertain if all strings got translated, that the translation agency did not miss any translations.

---

Naming: Is `checkTemperature` returning true when temperature is ok? Or when some action is needed? What does it do when it needs to warn? Try another name to express its purpose.

```c
assert(checkTemperature(33.0));
assert(!checkTemperature(-52.0));
```

---

Dynamically changing language at runtime is not needed, but it does make testing easier. Note the use of `SelectLanguageandWarnigMessage` [in this repo](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-c-azharmj/blob/4b9dc2ccc1106de063df24aa26c46d891decb4fe/checker.c), and `setPrintLanguage` in [this repo](https://github.com/clean-code-craft-tcq-7/simple-monitor-in-c-balasu-tcqtest/blob/6e82a49854a44a3cfdac5dfa386881594ee5afc7/test_cases.c).
Both have employed dynamic language selection, instead of compiler directives to change the language.

---

Consider tests for messages:

```c
    printTempratureMessage(LOW_VALUE_WARNING, &testPrintFunc);
    assert(strcmp(testString, "Low Temperature Warning\n") == 0);
    setPrintLanguage(GERMAN);
    printTempratureMessage(LOW_VALUE_WARNING, &testPrintFunc);
    assert(strcmp(testString, "Warnung vor niedriger Temperatur\n") == 0);
```

While these tests bring confidence that the texts are exactly as we intend them to be, they bring double-work: Any change in text has to be done twice now.

Think of a way to test the 'minimum required' behavior of the texts. For example: assert that they should mention the measure (temperature), it's status (low) and its severity (warning), checking for spelling and capitalization. That way, it can be made better / customized as per user's preferences, while still ensuring the basic health of the message.
