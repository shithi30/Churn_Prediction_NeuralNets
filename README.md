
## Neural Nets for Detecting Potential Churns and Power Users

*Note: Only models published, due to org's governance policy*

### Dataset
TallyKhata applied supervised classification (from its historical data) to tell if a user -- after registering and passing some days on the platform -- would churn or turn into a regular active user (RAU, also PU as some orgs would put it). To accomplish this, I prepared a training dataset containing the following:
- <strong>Identifiers:</strong> A phone no. or user id, by which a merchant could be uniquely identified
- <strong>Features:</strong> Esssesnce of the dataset, capturing tendencies within 7/14/21/42-day windows prior to the prediction timeframe, containing:
  - Platform info: reg. date, maturity of TK-platform
  - Version info: current/starting version, update records
  - Recent (in)activity weeks: Transactions recorded, customers/suppliers added, time spent
- <strong>Labels:</strong> Tendency of the merchant, in the upcoming 7/14 days

### Training
- Labels encoded one-hot
- Feed-forward NNs (input + ReLU + Softmax) Xavier-initialized
- Cross-entropy loss fuction Adam-optimized in mini-batches

Features were often tested inferentially for significance. Distribution of OP labels were also verified against training data, to make sure proper trainig took place.

<img width="640" alt="fl1" src="https://github.com/shithi30/Churn_Prediction_NeuralNets/assets/43873081/b7bb1488-64f9-4b36-a9f7-0083979aa947">

### Output & Analysis
The models were trained to answer BI questions like:
- Will a merchant churn (or, become a PU) in the next 7/14 days?
- Will a merchant's activity decline by >=30% soon?
- Will the merchant soon be investing lesser time on TK?

NN models developed at TK have answered these questions with a highest ~89% accuracy. After prediction, results were written on warehouse-tables, and business decisions were executed duly based on the output. Since merchants enter their financial data (cash/credit sales, returns, cashbox txns) in TK-app, the NNs also helped TallyKhata Digital Credit (TKDC) team to make decisions on merchants' credit-worthiness.
