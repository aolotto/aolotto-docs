# 🌟 Draw & Rules

Normally, each round of betting is open for 24 hours. The betting rate of the round needs to be greater than or equal to 100% to meet the conditions for a draw. The pool trigger will check every 2 minutes. The round that meets the conditions for the prize draw will automatically end, and then the next round will be started.

1. **The opening time is ≥ 24 hours**, and the difference between the end time and the start time must be ≥ 24 hours.
2. **The betting rate ≥ 100%**, When a round starts, 50% of the previous round's pool balance will be counted as the basic bonus. The betting rate = (total betting amount / basic bonus) \* 100%.

### **Round Switching**

As mentioned above, the betting rate of a round may not reach 100% within the expected time. If the opening time exceeds 24 hours, the round will exist in one of the following three states:

1. The opening time exceeds 24 hours, and the betting reaches 100%. The next round will start immediately, and the betting records of the current round will be archived, waiting for the draw.
2. If the opening time exceeds 24 hours but the betting rate does not meet the lottery conditions, the current round will remain open for new bets until the betting rate reaches ≥ 100%.
3. If the opening time exceeds 168 hours and the betting rate is still less than 100%, the round will be forcibly cancelled. Since the prize-drawing conditions are not met, all bets in this round will be returned to the users, and the basic prize money of this round will be transferred to the next round.
