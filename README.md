
const signals = [
  { pair: "EUR/JPY", signal: "BUY", entry: 164.25, exit: 164.40 },
  { pair: "GBP/USD", signal: "SELL", entry: 1.3020, exit: 1.3010 },
  { pair: "AUD/JPY", signal: "WAIT", entry: 98.20, exit: 98.20 }
];

let correct = 0;
let tested = 0;

for (const trade of signals) {
  let result = "SKIPPED";

  if (trade.signal !== "WAIT") {
    const movedUp = trade.exit > trade.entry;
    const movedDown = trade.exit < trade.entry;

    const won =
      (trade.signal === "BUY" && movedUp) ||
      (trade.signal === "SELL" && movedDown);

    result = won ? "WIN" : "LOSS";
    tested++;

    if (won) correct++;
  }

  console.log(
    `${trade.pair} | ${trade.signal} | ${result}`
  );
}

console.log(`Tested: ${tested}`);
console.log(`Wins: ${correct}`);
console.log(
  `Observed win rate: ${
    tested ? ((correct / tested) * 100).toFixed(2) + "%" : "N/A"
  }`
);
console.log("এটি শুধু উদাহরণ ডেটা; বাস্তব মার্কেট ফলাফল নয়।");
