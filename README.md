# Insert multiple values into the Oracle database when a checkbox is checked via a dynamic action in Oracle APEX, and display a confirmation message.
## APEX Page Setup
- Create a checkbox item and a button in APEX.

- Create a dynamic action for the button click event.

# Example Image

![alt text](image.png)

# Dynamic action PL/SQL Code

```PL/SQL code

DECLARE
    l_ids apex_t_varchar2;
    V_ID NUMBER;

BEGIN
    l_ids := apex_string.split(:P41_MENU, ':');

    FOR i IN 1 .. l_ids.COUNT LOOP
           
        SELECT NVL(MAX(ACCESS_ID),0)+1 INTO V_ID
        FROM USER_ACCESS;

      INSERT INTO USER_ACCESS (ACCESS_ID, PAGE_ID, P_USERID, INSERT_DATE, INSERT_BY,STATUS )
      VALUES(V_ID, l_ids(i), :P41_USER_ID, sysdate, :APP_USER, 1);
    END LOOP;

    --  show message
    apex_application.g_print_success_message := 'Access granted successfully.';
END;


```
 # Thank you
 ## Sanjay Sikder
