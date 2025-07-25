class WagerSystem:
    def __init__(self):
        self.bets = {'Yes': [], 'No': []}
        self.total_yes = 0
        self.total_no = 0

    def place_bet(self, outcome, amount, user):
        if outcome == 'Yes':
            self.bets['Yes'].append((user, amount))
            self.total_yes += amount
        elif outcome == 'No':
            self.bets['No'].append((user, amount))
            self.total_no += amount
        else:
            raise ValueError("Invalid outcome")
        print(f"Bet placed: {user} bets {amount} on {outcome}")

    def resolve(self, actual_outcome):
        total_pool = self.total_yes + self.total_no
        if actual_outcome == 'Yes':
            winners = self.bets['Yes']
            winner_total = self.total_yes
        elif actual_outcome == 'No':
            winners = self.bets['No']
            winner_total = self.total_no
        else:
            raise ValueError("Invalid resolution")

        if winner_total == 0:
            print("No winners")
            return

        for user, amount in winners:
            payout = (amount / winner_total) * total_pool
            print(f"{user} wins {payout:.2f}")

# Usage example:
# system = WagerSystem()
# system.place_bet('Yes', 100, 'User1')
# system.place_bet('No', 200, 'User2')
# system.place_bet('Yes', 150, 'User3')
# system.resolve('Yes')
