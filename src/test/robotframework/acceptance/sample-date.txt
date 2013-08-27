*** Settings ***
Library     JSpringBotGlobal
Library     BuiltIn

*** Test Cases ***

Date Keyword Sample Usage
    [Tags]      date-keywords
    Set Date Time Zone          Japan
    Print Date Time
    Set Date Time Format        dd-MM-yyyy HH:mm
    Print Date Time
    Format Date Time
    Add Date Time Days          90
    Print Date Time
    Subtract Date Time Days     40
    Print Date Time
    Parse Date Time             2013-02-08      yyyy-MM-dd
    Print Date Time
    Reset Date Time
    Print Date Time

Date Functions Sample Usage
    [Tags]      date-functions
    ${dateNow}=             EL Evaluate                                         $[date:now()]
    ${currentNow}=          EL Evaluate                                         $[date:current()]
    Set Date Time Format    yyyy-MM-dd HH:mm:ss
    Set Date Time Zone      Asia/Taipei
    EL Should Be Equal      $[date:parse('2013-02-08', 'yyyy-MM-dd')]           2013-02-08 00:00:00
    EL Should Be Equal      $[date:current('+1d +1y -1M')]                      2014-01-09 00:00:00
    ${sqlDate}=                     EL Evaluate                                 $[date:toSQLDate()]
    ${sqlTime}=                     EL Evaluate                                 $[date:toSQLTime()]
    ${sqlTimestamp}=                EL Evaluate                                 $[date:toSQLTimestamp()]
    Should Be Equal As Strings      ${sqlDate}                                  2013-02-08
    Should Be Equal As Strings      ${sqlTime}                                  00:00:00
    Should Be Equal As Strings      ${sqlTimestamp}                             2013-02-08 00:00:00.0
    ${sqlDate}=                     EL Evaluate                                 $[date:toSQLDate('2013-03-08', 'yyyy-MM-dd')]
    ${sqlTime}=                     EL Evaluate                                 $[date:toSQLTime()]
    ${sqlTimestamp}=                EL Evaluate                                 $[date:toSQLTimestamp()]
    Should Be Equal As Strings      ${sqlDate}                                  2013-03-08
    Should Be Equal As Strings      ${sqlTime}                                  00:00:00
    Should Be Equal As Strings      ${sqlTimestamp}                             2013-03-08 00:00:00.0
    ${firstDayOfMonth}=             EL Evaluate                                 $[date:firstDayOfMonth()]
    ${lastDayOfMonth}=              EL Evaluate                                 $[date:lastDayOfMonth()]
    ${firstDayOfYear}=              EL Evaluate                                 $[date:firstDayOfYear()]
    EL Should Be Equal              $[date:isoParse('2013-03-18T15:39:43.000+08:00')]   2013-03-18 15:39:43
    EL Should Be Equal              $[date:changeISODateFormat('2013-03-18T15:39:43.000+08:00','yyyy-MM-dd HH:mm:ss.S')]    2013-03-18 15:39:43.0
    EL Should Be True               $[date:isBeforeNow()]

ISO Date Format
    [Tags]      iso-date-format
    Set Date Time Zone          Asia/Taipei
    Print Date Time
    Set Date Time Format        yyyy-MM-dd'T'HH:mm:ss.SSSZ
    Print Date Time
    ${currentNow}=              EL Evaluate                                     $[date:current()]
    Add Date Time Days          1
    ${tomorrow}=                EL Evaluate                                     $[date:current()]
