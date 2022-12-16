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

Complexity of 4:

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

...is an indication to write concisely

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

