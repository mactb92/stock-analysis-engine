IEX API
=======

IEX - Account Set Up
====================

#.  `Register for an Account <https://iexcloud.io/cloud-login/#/register>`__

#.  Set ``IEX_TOKEN`` the Environment Variable

    ::

        export IEX_TOKEN=PUBLISHABLE_TOKEN

IEX - Get Data
==============

Use this function to pull data from IEX with a shared API for supported fetch routines over the IEX HTTP Rest API.

.. automodule:: analysis_engine.iex.get_data
   :members: get_data_from_iex

IEX - Fetch Data
================

This is a helper for the parent method:

``analysis_engine.iex.get_data.py``

.. automodule:: analysis_engine.iex.fetch_data
   :members: fetch_data

IEX - HTTP Fetch Functions
==========================

.. automodule:: analysis_engine.iex.helpers_for_iex_api
   :members: get_from_iex,handle_get_from_iex,get_from_iex_cloud,get_from_iex_v1,convert_datetime_columns

IEX - Build Auth URL Using Publishable Token
============================================

.. automodule:: analysis_engine.iex.build_auth_url
   :members: build_auth_url

IEX - Fetch Common Utilities
============================

.. automodule:: analysis_engine.iex.fetch_api
   :members: fetch_daily,fetch_minute,fetch_quote,fetch_stats,fetch_stats,fetch_news,fetch_financials,fetch_earnings,fetch_dividends,fetch_company

Default Fields
--------------

.. automodule:: analysis_engine.iex.get_default_fields
   :members: get_default_fields

IEX - Dataset Extraction API
============================

Here is the extraction API for returning a ``pandas.DataFrame`` from cached or archived IEX datasets.

.. automodule:: analysis_engine.iex.extract_df_from_redis
   :members: extract_daily_dataset,extract_minute_dataset,extract_quote_dataset,extract_stats_dataset,extract_peers_dataset,extract_news_dataset,extract_financials_dataset,extract_earnings_dataset,extract_dividends_dataset,extract_company_dataset

IEX API Example - Fetch Minute Intraday Data using HTTP
=======================================================

.. warning:: This will fetch ``minute`` data using your IEX Cloud account and can cost money depending on your request usage.

.. code-block:: python

    import analysis_engine.iex.fetch_api as fetch
    df = fetch.fetch_minute(ticker='SPY')
    print(df)

IEX API Example - Extract Minute Intraday Data from Cache
=========================================================

.. code-block:: python

    import datetime
    import analysis_engine.iex.extract_df_from_redis as extract
    ticker = 'SPY'
    today = datetime.datetime.now().strftime('%Y-%m-%d')
    status, df = extract.extract_minute_dataset({
        'ticker': f'{ticker}',
        'redis_key': f'{ticker}_{today}_minute'})
    print(df)

IEX API Example - Get Minute Data from IEX (calls fetch and cache)
==================================================================

.. warning:: This will fetch and cache ``minute`` data using your IEX Cloud account and can cost money depending on your request usage.

.. code-block:: python

    import analysis_engine.iex.get_data as get_data
    df = get_data.get_data_from_iex({
        'ticker': 'SPY',
        'ft_type': 'minute'})
    print(df)
