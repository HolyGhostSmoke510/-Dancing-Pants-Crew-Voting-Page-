# -Dancing-Pants-Crew-Voting-Page-
Here’s a way we can vote people!
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Group Voting</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      text-align: center;
      padding: 30px;
    }

    h1 {
      margin-bottom: 20px;
    }

    .option {
      background: white;
      margin: 10px auto;
      padding: 15px;
      width: 300px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    button {
      margin-top: 10px;
      padding: 8px 15px;
      border: none;
      border-radius: 5px;
      background: #007bff;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background: #0056b3;
    }

    .results {
      margin-top: 8px;
      font-size: 14px;
    }
  </style>
</head>
<body>

<h1>Vote for Our Next Hangout 🎉</h1>

<div id="options"></div>

<script>
  const options = [
    "Lake picnic",
    "Bonfire at the beach",
    "Mini hike / Nice view",
    "Tennis get together (DeFremery Park West Oakland)",
    "Skate park (Berkeley)"
  ];

  let votes = JSON.parse(localStorage.getItem("votes")) || [0,0,0,0,0];

  function saveVotes() {
    localStorage.setItem("votes", JSON.stringify(votes));
  }

  function getTotalVotes() {
    return votes.reduce((a, b) => a + b, 0);
  }

  function vote(index) {
    votes[index]++;
    saveVotes();
    render();
  }

  function render() {
    const container = document.getElementById("options");
    container.innerHTML = "";

    const total = getTotalVotes();

    options.forEach((option, index) => {
      const percent = total === 0 ? 0 : ((votes[index] / total) * 100).toFixed(1);

      const div = document.createElement("div");
      div.className = "option";

      div.innerHTML = `
        <strong>${option}</strong><br>
        <button onclick="vote(${index})">Vote</button>
        <div class="results">
          Votes: ${votes[index]} <br>
          Percentage: ${percent}%
        </div>
      `;

      container.appendChild(div);
    });

    const totalDiv = document.createElement("div");
    totalDiv.style.marginTop = "20px";
    totalDiv.innerHTML = `<strong>Total Votes: ${total}</strong>`;
    container.appendChild(totalDiv);
  }

  render();
</script>

</body>
</html>
