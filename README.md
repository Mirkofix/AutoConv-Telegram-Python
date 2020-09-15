# Setup

```
pip3 install telegram-autoconv
```

# Requirements
* Python 3.8

# Import
```python
from autoconv.state import State
from autoconv.conversation import Conversation
from autoconv.autoconv_handler import AutoConvHandler
```

# Documentation
I know you want examples, in fact there is a beautiful folder with some examples.  
But here, you can find a little documentation.

### State
```python
State(name,message,type=int,parse_mode=None)
```
- `name`: State name (and key for data dictionary). {`str`}
- `message`: message you want to print in that state. {`str`}
- `type`: data type. {`type`}
- `parse_mode`: Telegram message parse mode. {`Telegram.parse_mode`}

```python
# callback handler
add_keyboard(keyboard,size=None)
```
- `keyboard`: inline keyboard. Can be a dict (with custom value as key) or a list (default int value as key). {`name list` or `value:name dict`}
- `size`: size for each row of the keyboard. {`int tuple`}

```python
# text handler
add_text(regex=None,error_message=None)
```
- `regex`: regex for input text. {`str`}
- `error_message`: error message when regex fails. {`str`}

```python
# function to execute in this state
add_action(function)
```
- `function`: function must have two parameters (`update` and `context`). It can return a `str`, repleacing 3 `@` (`@@@`) in the message. {`func`}

### Conversation
```python
Conversation(start_state,end_state=None)
```
- `start_state`: first State of the conversation. {`State`}
- `end_state`: if exists, final State of the conversation. {`State`}

```python
# add state to the conversation
add_state(State)
```
- `State`: Add a State or a list of State to the conversation. {`State` or `State list`}

```python
# add state to the conversation
add_route(state,ruotes=None,default=None,back=None)
```
- `state`: initial State of the ruote. {`State`}
- `routes`: routes where a state should go for every possibile data received. {`value:State dict`}
- `default`: default route if value isn't in ruotes. {`State`}
- `back`: route to go when the back button is pressed. {`State`}

### AutoConvHandler
```python
AutoConvHandler(conversation,telegram_state,back_button=None)
```
- `conversation`: conversation to handle. {`Conversation`}
- `telegram_state`: Telegram state name to handle callback, text and other things. {`Telegram.handler`}
- `back_button`: default back button for every State. {`str`}

```python
# manage conversation with update and context
manage_conversation(update,context)
```
- `update` e `context`: update and context from the telegram bot function. {`Telegram.update` and `Telegram.context`}
