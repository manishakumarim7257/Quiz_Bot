# Quiz_Bot 🎯

A powerful **Telegram Quiz Bot** built with Python that allows users to create custom quizzes and play them with friends. The bot uses SQLite database for persistent storage and supports interactive quiz creation and gameplay.

## Features ✨

- **Create Custom Quizzes**: Users can create quizzes with custom questions, options, and explanations
- **Play Quizzes**: Play saved quizzes by ID with randomized question order
- **Database Storage**: SQLite database to store quizzes, questions, and user data
- **Interactive UI**: User-friendly keyboard interface with Telegram Reply Keyboards
- **Score Tracking**: Automatic score calculation during quiz gameplay
- **Explanations**: Detailed explanations for correct answers after each question
- **Admin Panel**: Owner-only stats panel to view bot usage
- **Hindi/Urdu Support**: Messages in Hinglish for better user experience
- **Conversation Handler**: Smooth state management for quiz creation and playing flows

## Project Structure 📁

```
Quiz_Bot/
├── quiz_bot.py          # Main bot application
├── requirements.txt     # Python dependencies
├── sample.env          # Environment variables template
├── README.md           # This file
└── LICENSE             # License file
```

## Installation 🚀

### Prerequisites
- Python 3.8 or higher
- A Telegram Bot Token (get from [@BotFather](https://t.me/botfather))
- Your Telegram User ID

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/manishakumarim7257/Quiz_Bot.git
   cd Quiz_Bot
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Create .env file**
   ```bash
   cp sample.env .env
   ```

4. **Configure .env file**
   - Add your `BOT_TOKEN` from [@BotFather](https://t.me/botfather)
   - Add your `OWNER_ID` (your Telegram user ID)
   
   ```
   BOT_TOKEN=your_bot_token_here
   OWNER_ID=your_user_id_here
   ```

5. **Run the bot**
   ```bash
   python quiz_bot.py
   ```

## Usage 💡

### Bot Commands

| Command | Description |
|---------|-------------|
| `/start` | Welcome message and command list |
| `/help` | Show help information |
| `/create` | Start creating a new quiz |
| `/play_id [ID]` | Play a quiz by its ID |
| `/cancel` | Cancel ongoing quiz creation/playing |
| `/stats` | View bot statistics (Owner only) |

### Creating a Quiz 📝

1. Send `/create` command
2. Enter quiz title
3. Enter quiz description
4. Add questions one by one with:
   - Question text
   - Options (minimum 2, maximum 4)
   - Select correct answer from buttons
   - Add explanation (or skip with `/skip`)
5. Choose to add more questions or save the quiz
6. After saving, you'll get a Quiz ID to share with others

### Playing a Quiz 🎮

1. Send `/play_id [quiz_id]` (e.g., `/play_id 1`)
2. Bot will show each question with options
3. Click on the correct answer
4. After all questions, you'll see your final score
5. Explanations are shown for incorrect answers

## Database Schema 🗄️

### Users Table
```sql
CREATE TABLE users (
    user_id INTEGER PRIMARY KEY,
    username TEXT,
    score INTEGER DEFAULT 0
)
```

### Quizzes Table
```sql
CREATE TABLE quizzes (
    quiz_id INTEGER PRIMARY KEY AUTOINCREMENT,
    creator_id INTEGER,
    title TEXT,
    description TEXT
)
```

### Questions Table
```sql
CREATE TABLE questions (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    quiz_id INTEGER,
    question_text TEXT,
    options TEXT (JSON),
    correct_answer TEXT,
    explanation TEXT,
    FOREIGN KEY(quiz_id) REFERENCES quizzes(quiz_id)
)
```

## Technologies Used 🛠️

- **Python 3.x** - Programming language
- **python-telegram-bot (21.10)** - Telegram Bot API wrapper
- **SQLite3** - Database
- **python-dotenv (1.0.1)** - Environment variable management

## Dependencies 📦

```
python-telegram-bot==21.10
python-dotenv==1.0.1
```

## Project Flow 🔄

### Quiz Creation Flow
```
/create → Title → Description → Add Question → Add Options → 
Select Correct Answer → Add Explanation → Save Quiz or Add More Questions
```

### Quiz Playing Flow
```
/play_id [ID] → Display Questions → User Answer → Check Answer → 
Show Score & Explanations → Next Question → Final Score
```

## Key Functions 🔧

- `init_db()` - Initialize SQLite database with required tables
- `create_quiz_start()` - Start quiz creation process
- `create_add_question()` - Add question to quiz
- `handle_creation_choice()` - Handle user choice during quiz creation
- `play_quiz_by_id()` - Load and start playing a quiz
- `send_next_db_question()` - Display next question during quiz
- `handle_db_quiz_answer()` - Process user's answer
- `stats()` - Show bot statistics (Owner only)

## Features Overview 🎪

### State Machine
The bot uses Telegram's ConversationHandler for managing:
- **CREATE_TITLE** → **CREATE_DESC** → **ADD_QUESTION** → **ADD_OPTIONS** → **ADD_CORRECT** → **ADD_EXPLANATION**
- **PLAYING_QUIZ** - For handling quiz gameplay

### Database Integration
- Persistent storage of quizzes and questions
- JSON serialization for storing multiple-choice options
- Support for quiz descriptions and explanations

### User Experience
- Emoji-enhanced messages in Hinglish
- Keyboard buttons for easy selection
- One-time keyboards to prevent accidental re-submission
- Automatic question shuffling for variety
- Score tracking and result display

## Future Enhancements 🚀

- [ ] User leaderboard
- [ ] Quiz categories
- [ ] Difficulty levels
- [ ] Time-limited questions
- [ ] Multiplayer mode
- [ ] Quiz sharing via links
- [ ] Analytics and reporting
- [ ] Export quizzes as PDF

## Troubleshooting 🐛

**Bot not responding?**
- Verify BOT_TOKEN is correct
- Check internet connection
- Ensure bot is running: `python quiz_bot.py`

**Quiz ID not found?**
- Make sure the quiz_id is correct
- Check if quiz exists in database
- Verify quiz was saved successfully

**Database errors?**
- Delete `quiz_bot.db` and restart to reinitialize
- Check file permissions in the directory

## License 📜

This project is licensed under the MIT License - see the LICENSE file for details.

## Author 👨‍💻

Created by **manishakumarim7257**

## Support & Contribution 🤝

Feel free to:
- Report issues
- Suggest improvements
- Create pull requests
- Share your feedback

---

**Happy Quizzing!** 🎉
