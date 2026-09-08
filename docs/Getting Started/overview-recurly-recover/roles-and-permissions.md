---
title: Roles and permissions
excerpt: >-
  How Recurly Recover provisions admin access and the four permission categories
  you combine to build roles for your team.
deprecated: false
hidden: false
metadata:
  robots: index
---
<div class="rp-page">
  <div class="rp-overview">Recurly Recover controls who can see and change what through roles built from permission categories. An Admin user creates roles, assigns them to invited users, and each user gets access only to the pages their role grants. This page covers how admin access is provisioned, the four permission categories a role can combine, and who can manage roles.</div>
  <div class="rp-plan"><i class="fa-solid fa-key" aria-hidden="true"></i> Available as a standalone product — Recurly Subscriptions is not required</div>
  <div class="rp-toc">
    <a class="rp-toc-pill" href="#how-admin-access-is-provisioned"><span class="rp-toc-num">1</span>How admin access is provisioned</a>
    <a class="rp-toc-pill" href="#permission-categories"><span class="rp-toc-num">2</span>Permission categories</a>
    <a class="rp-toc-pill" href="#faqs"><span class="rp-toc-num">3</span>FAQs</a>
  </div>
</div>

<div class="rp-callout rp-callout-note">
  <div><strong><i class="fa-solid fa-circle-info" aria-hidden="true"></i> Note</strong> This page describes Recover's current (stop-gap) roles and permissions model. A full custom-role system is planned; until then, access is managed through the four permission categories below.</div>
</div>

# How admin access is provisioned

<div class="rp-steps">
  <div class="rp-step">
    <div class="rp-step-num">1</div>
    <div><h4>Your site is provisioned on a Recover plan</h4><p>Recurly configures your merchant account on either the <strong>Recurly Recover Annual Monthly</strong> or <strong>Recurly Recover Monthly</strong> plan.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">2</div>
    <div><h4>The Admin user logs in</h4><p>Because the account is subscribed to a Recover plan, this user sees the Recover UI and navigation. Until roles are created, they see only the <strong>Admin</strong> navigation link and page.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">3</div>
    <div><h4>The Admin creates roles</h4><p>Using <strong>Admin &rarr; Roles</strong>, the Admin user builds one or more roles from the permission categories below.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">4</div>
    <div><h4>The Admin invites users and assigns roles</h4><p>Each invited user is assigned one of the roles created in the previous step.</p></div>
  </div>
  <div class="rp-step">
    <div class="rp-step-num">5</div>
    <div><h4>Users get access based on their role</h4><p>New users can reach only the pages granted by the permission categories on their assigned role. Every user — regardless of role — has access to the Recover dashboard.</p></div>
  </div>
</div>

# Permission categories

A role can combine any number of these four categories:

<table class="rp-gw-table">
  <tr class="rp-thead-row"><td>Category</td><td>Grants access to</td></tr>
  <tr>
    <td>Analytics &amp; Insights</td>
    <td>
      <ul class="rp-list">
        <li>Recovered revenue</li>
        <li>Payment processing</li>
        <li>Retry &amp; recovery</li>
        <li>Campaign performance</li>
        <li>Invoices</li>
        <li>Transactions</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Configuration</td>
    <td>
      <ul class="rp-list">
        <li>Payment gateway settings — view and edit</li>
        <li>Retention (retry window) settings — view and edit</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Integrations</td>
    <td>
      <ul class="rp-list">
        <li>API credentials — view and edit</li>
        <li>Webhooks — view and edit</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Admin</td>
    <td>
      <ul class="rp-list">
        <li>Users</li>
        <li>Roles</li>
      </ul>
    </td>
  </tr>
</table>

<div class="rp-callout rp-callout-tip">
  <div><strong><i class="fa-solid fa-lightbulb" aria-hidden="true"></i> Tip</strong> Mix categories to fit the job. A finance teammate's role might combine Analytics &amp; Insights with Configuration, while a developer's role might combine Integrations with Analytics &amp; Insights.</div>
</div>

# FAQs

<Accordion title="Who can create and assign roles in Recurly Recover?" icon="fa-solid fa-user-shield">
  Only a user with the Admin permission category can create roles and invite or assign users. Every user granted access — regardless of role — automatically has access to the Recover dashboard.
</Accordion>
