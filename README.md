from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/chat', methods=['GET', 'POST'])
def chat():
    if request.method == 'POST':
        user_message = request.form['message']
        # Add chat handling logic here
        response = f'You said: {user_message}'
        return render_template('chat.html', response=response)
    return render_template('chat.html')

@app.route('/topics')
def topics():
    return render_template('topics.html')

@app.route('/topics/<topic>')
def topic_details(topic):
    # Add logic to fetch topic details here
    return render_template('topic_details.html', topic=topic)

if __name__ == '__main__':
    app.run(debug=True){% extends "base.html" %}

{% block title %}Chat{% endblock %}

{% block content %}
    <h1>Chat</h1>
    <form method="POST">
        <input type="text" name="message" placeholder="Type your message">
        <button type="submit">Send</button>
    </form>
    {% if response %}
        <p>{{ response }}</p>
    {% endif %}
{% endblock %}{% extends "base.html" %}

{% block title %}Topics{% endblock %}

{% block content %}
    <h1>Topics</h1>
    <ul>
        <li><a href="/topics/ethical-hacking">Ethical Hacking</a></li>
        <li><a href="/topics/python">Python</a></li>
        <li><a href="/topics/java">Java</a></li>
    </ul>
{% endblock %}{% extends "base.html" %}

{% block title %}{{ topic }}{% endblock %}

{% block content %}
    <h1>{{ topic }}</h1>
    <p>Information about {{ topic }} will be here.</p>
{% endblock %}<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}{% endblock %}</title>
</head>
<body>
    <header>
        <h1>Educational App</h1>
        <nav>
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/chat">Chat</a></li>
                <li><a href="/topics">Topics</a></li>
            </ul>
        </nav>
    </header>
    <main>
        {% block content %}{% endblock %}
    </main>
    <footer>
        <p>&copy; 2025 Educational App</p>
    </footer>
</body>
</html>mkdir educational_app
cd educational_appmkdir templatespip install flaskpython app.pyhttp://127.0.0.1:5000/
