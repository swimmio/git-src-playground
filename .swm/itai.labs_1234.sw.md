---
id: labs_1234
name: Adding a Host Exploiter
file_version: 1.0.2
app_version: 0.6.9-2
file_blobs:
  monkey/monkey_island/cc/ui/src/components/report-components/SecurityReport.js: 2850af42d990e27dabf6b3f1c4c4daab8bcd2907
  envs/monkey_zoo/blackbox/config_templates/tunneling.py: 15fb967d57d5a71c5e2e687f77c314871adc746e
  monkey/monkey_island/cc/services/config_schema/basic.py: a9eb03d62f5f1ce333e7f5a64aeddac283d7b197
  monkey/infection_monkey/exploit/powershell.py: f2883bb63e50ae085270074edc78d908af202c04
  envs/monkey_zoo/blackbox/config_templates/performance.py: 07c7cd79f8ac492018c359a2e326078ace7c5fd4
  monkey/infection_monkey/example.conf: dcb3b31388e6817439f6e06417436be3a00a800a
  monkey/monkey_island/cc/services/reporting/issue_processing/exploit_processing/exploiter_descriptor_enum.py: 44e0c922a51f5fe96e52f399a4f7b63f58d0d0bc
  monkey/monkey_island/cc/services/config_schema/definitions/exploiter_classes.py: 44463bbcdffd87e493da619dd006fb4080e4cc68
---

Adding a Host Exploiter
===================

In this document, we will learn how to add a new `HostExploiter` to the system.

A `HostExploiter` is 🙋‍

Some examples of `HostExploiter`s are `MSSQLExploiter` and `Ms08_067_Exploiter`.




## Basic Example

We'll follow the implementation of `PowerShellExploiter` for this example.

`PowerShellExploiter` is 🙋

### TL;DR

1. Create a new class inheriting from `HostExploiter`&nbsp;
   - Place the file under `📄 monkey/infection_monkey/exploit`<br />
     e.g. `PowerShellExploiter` is defined in `📄 monkey/infection_monkey/exploit/powershell.py`.
2. Define `_TARGET_OS_TYPE` and `_EXPLOITED_SERVICE`
2. Implement `_exploit_host` and `__init__`

3. Update `📄 monkey/monkey_island/cc/services/config_schema/definitions/exploiter_classes.py`
3. Update `📄 monkey/monkey_island/cc/ui/src/components/report-components/SecurityReport.js`
3. Update `📄 monkey/monkey_island/cc/services/reporting/issue_processing/exploit_processing/exploiter_descriptor_enum.py`
3. Update `📄 envs/monkey_zoo/blackbox/config_templates/performance.py`
3. Update `📄 monkey/monkey_island/cc/services/config_schema/basic.py`

4. **Profit** 💰

## 1. Inherit from `HostExploiter`
All `HostExploiter`s are defined in files under `📄 monkey/infection_monkey/exploit`.

<br/>

We first need to define our class in the relevant file, and inherit from `HostExploiter`:
<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/infection_monkey/exploit/powershell.py
```python
⬜ 36         pass
⬜ 37     
⬜ 38     
🟩 39     class PowerShellExploiter(HostExploiter):
⬜ 40         _TARGET_OS_TYPE = ["windows"]
⬜ 41         EXPLOIT_TYPE = ExploitType.BRUTE_FORCE
⬜ 42         _EXPLOITED_SERVICE = "PowerShell Remoting (WinRM)"
```

<br/>


> **Note**: the class name should end with "Exploiter".

## 2. Define `_TARGET_OS_TYPE` and `_EXPLOITED_SERVICE`
Every `HostExploiter` should define these variables:
- `_TARGET_OS_TYPE`: 🙋‍
- `_EXPLOITED_SERVICE`: 🙋‍

    <br/>

    <!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/infection_monkey/exploit/powershell.py
```python
⬜ 37     
⬜ 38     
⬜ 39     class PowerShellExploiter(HostExploiter):
🟩 40         _TARGET_OS_TYPE = ["windows"]
⬜ 41         EXPLOIT_TYPE = ExploitType.BRUTE_FORCE
🟩 42         _EXPLOITED_SERVICE = "PowerShell Remoting (WinRM)"
⬜ 43     
⬜ 44         def __init__(self, host: VictimHost):
⬜ 45             super().__init__(host)
```

<br/>


## 3. Implement `_exploit_host`
The goal of `_exploit_host` is to 🙋.

<br/>

In this example, `PowerShellExploiter`, we 🙋
<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/infection_monkey/exploit/powershell.py
```python
⬜ 45             super().__init__(host)
⬜ 46             self._client = None
⬜ 47     
🟩 48         def _exploit_host(self):
⬜ 49             try:
⬜ 50                 use_ssl = self._is_client_using_https()
⬜ 51             except PowerShellRemotingDisabledError as e:
```

<br/>

## 4. Implement `__init__`
The goal of `__init__` is to 🙋.

<br/>

In this example, `PowerShellExploiter`, we 🙋
<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/infection_monkey/exploit/powershell.py
```python
⬜ 41         EXPLOIT_TYPE = ExploitType.BRUTE_FORCE
⬜ 42         _EXPLOITED_SERVICE = "PowerShell Remoting (WinRM)"
⬜ 43     
🟩 44         def __init__(self, host: VictimHost):
🟩 45             super().__init__(host)
🟩 46             self._client = None
⬜ 47     
⬜ 48         def _exploit_host(self):
⬜ 49             try:
```

<br/>



## 5. Update `📄 exploiter_classes.py`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/monkey_island/cc/services/config_schema/definitions/exploiter_classes.py
```python
⬜ 138            },
⬜ 139            {
⬜ 140                "type": "string",
🟩 141                "enum": ["PowerShellExploiter"],
⬜ 142                "title": "PowerShell Remoting Exploiter",
⬜ 143                "info": "Exploits PowerShell remote execution setups. PowerShell Remoting uses Windows "
⬜ 144                "Remote Management (WinRM) to allow users to run PowerShell commands on remote "
```

<br/>

## 6. Update `📄 SecurityReport.js`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/monkey_island/cc/ui/src/components/report-components/SecurityReport.js
```python
⬜ 130            [this.issueContentTypes.REPORT]: shellShockIssueReport,
⬜ 131            [this.issueContentTypes.TYPE]: this.issueTypes.DANGER
⬜ 132          },
🟩 133          'PowerShellExploiter': {
⬜ 134            [this.issueContentTypes.OVERVIEW]: powershellIssueOverview,
⬜ 135            [this.issueContentTypes.REPORT]: powershellIssueReport,
⬜ 136            [this.issueContentTypes.TYPE]: this.issueTypes.DANGER
```

<br/>

## 7. Update `📄 exploiter_descriptor_enum.py`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/monkey_island/cc/services/reporting/issue_processing/exploit_processing/exploiter_descriptor_enum.py
```python
⬜ 46             "ZerologonExploiter", "Zerologon Exploiter", ZerologonExploitProcessor
⬜ 47         )
⬜ 48         POWERSHELL = ExploiterDescriptor(
🟩 49             "PowerShellExploiter", "PowerShell Remoting Exploiter", ExploitProcessor
⬜ 50         )
⬜ 51     
⬜ 52         @staticmethod
```

<br/>

## 8. Update `📄 performance.py`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 envs/monkey_zoo/blackbox/config_templates/performance.py
```python
⬜ 22                 "WebLogicExploiter",
⬜ 23                 "HadoopExploiter",
⬜ 24                 "MSSQLExploiter",
🟩 25                 "PowerShellExploiter",
⬜ 26                 "ZerologonExploiter",
⬜ 27             ],
⬜ 28             "basic_network.network_analysis.inaccessible_subnets": [
```

<br/>

## 9. Update `📄 basic.py`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/monkey_island/cc/services/config_schema/basic.py
```python
⬜ 24                             "HadoopExploiter",
⬜ 25                             "MSSQLExploiter",
⬜ 26                             "DrupalExploiter",
🟩 27                             "PowerShellExploiter",
⬜ 28                         ],
⬜ 29                     }
⬜ 30                 },
```

<br/>


## Optional
### 3. Update `📄 example.conf`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 monkey/infection_monkey/example.conf
```python
⬜ 24       "dropper_target_path_linux": "/tmp/monkey",
⬜ 25     
⬜ 26       "exploiter_classes": [
🟩 27         "SSHExploiter",
⬜ 28         "SmbExploiter",
⬜ 29         "WmiExploiter",
⬜ 30         "ShellShockExploiter",
```

<br/>

### 3. Update `📄 tunneling.py`
<br/>

<!-- NOTE-swimm-snippet: the lines below links your snippet to Swimm -->
### 📄 envs/monkey_zoo/blackbox/config_templates/tunneling.py
```python
⬜ 9      
⬜ 10         config_values.update(
⬜ 11             {
🟩 12                 "basic.exploiters.exploiter_classes": ["SmbExploiter", "WmiExploiter", "SSHExploiter"],
⬜ 13                 "basic_network.scope.subnet_scan_list": [
⬜ 14                     "10.2.2.9",
⬜ 15                     "10.2.1.10",
```

<br/>

<!--
Each file consists of one class, and the file's name resembles the name of the class.


As an example, let's look at MyPBA .
In this example, we inherit from ...:
<snippet>

    We need to implement the method my_method .

    We then add the name of the class within `file.py`:
    (snippet)

    We don 't always inherit from PBA... or a subclass of PBA such as X,Y.:. Most inherit from `X`.
    (optionally - describe hierarchy)
-->
