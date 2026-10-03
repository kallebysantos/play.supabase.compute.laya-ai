# Supabase Compute + Laya

Self-hosting an Open Source Jev in Supabase Compute

## Getting started

**Deploying to Supabase**

```bash
supabase link
supabase compute push
```

**Running predicts**

> [!WARNING]
> The 1º inference may take up to minutes as it need to warm the AI model, but then it get very fast `~2s`

You can access the Frontend page directly `https://<project_ref>.supabase.com/compute/v1/laya/`
or call from API `/predict`

```bash
curl -s https://<project_ref>.supabase.com/compute/v1/laya/predict -H 'content-type: application/json' -d '{
        "state": {"from": "user@acme.com",
                  "subject": "Duplicate charge on invoice #4411",
                  "body": "We were billed twice for March. Please refund it today or we will cancel."},
        "questions": {
          "department": {"type": "choice",
                         "instructions": "Which department should handle this request?",
                         "criteria": {"billing": "invoices, payments, refunds",
                                      "technical": "bugs, outages, system errors",
                                      "sales": "pricing, new contracts",
                                      "other": "everything else"}},
          "urgency": {"type": "score",
                      "instructions": "How urgent is this request?",
                      "criteria": ["not urgent", "soon", "critical deadline or blocking issue"]},
          "churn_risk": {"type": "noul",
                         "instructions": "Does the user threaten to cancel or leave?"}
        }
      }'
```
