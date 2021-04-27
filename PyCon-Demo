{
    "metadata": {
        "kernelspec": {
            "name": "python3",
            "display_name": "Python 3",
            "language": "python"
        },
        "language_info": {
            "name": "python",
            "version": "3.6.8",
            "mimetype": "text/x-python",
            "codemirror_mode": {
                "name": "ipython",
                "version": 3
            },
            "pygments_lexer": "ipython3",
            "nbconvert_exporter": "python",
            "file_extension": ".py"
        }
    },
    "nbformat_minor": 2,
    "nbformat": 4,
    "cells": [
        {
            "cell_type": "markdown",
            "source": [
                "# Testing Kqlmagic with Parameterized query\n",
                "The purpose of this notebook is to query Samples database in the Help ADX cluster. The default parameter is set to GEORGIA. When invoking this notebook, users can change the filter to something else.\n",
                "The login is provided with az cli. If users already logged in, they won't have to do SSO anymore."
            ],
            "metadata": {
                "azdata_cell_guid": "20381b60-8ed9-4c00-b61c-4f04e0b9f8b0"
            }
        },
        {
            "cell_type": "markdown",
            "source": [
                "## Set the State Filter parameter\n",
                "\n",
                "Default value for stateFilter is GEORGIA. It can be set to something else."
            ],
            "metadata": {
                "azdata_cell_guid": "a7387bee-4449-457d-a52a-17a23f62acab"
            }
        },
        {
            "cell_type": "code",
            "source": [
                "stateFilter = \"GEORGIA\";"
            ],
            "metadata": {
                "azdata_cell_guid": "7cd71a72-6990-403e-bc90-f88e7aa8d059",
                "tags": [
                    "parameters"
                ]
            },
            "outputs": [],
            "execution_count": 2
        },
        {
            "cell_type": "markdown",
            "source": [
                "## Load Kqlmagic first\r\n",
                "\r\n",
                "This assumes that Kqlmagic has been installed."
            ],
            "metadata": {
                "azdata_cell_guid": "2bec6e83-8dec-448c-bc73-13ec7b79df27"
            }
        },
        {
            "cell_type": "code",
            "source": [
                "%reload_ext Kqlmagic"
            ],
            "metadata": {
                "azdata_cell_guid": "662ad3dd-5934-4265-976a-8c0d18cc9676"
            },
            "outputs": [
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<html>\n            <head>\n            <title>Kqlmagic - banner</title>\n            <style>\n            .kql-magic-banner {\n                display: flex; \n                background-color: #d9edf7;\n            }\n            .kql-magic-banner > div {\n                margin: 10px; \n                padding: 20px; \n                color: #3a87ad; \n                font-size: 13px;\n            }\n            </style>\n            </head>\n            <body>\n                <div class='kql-magic-banner'>\n                    <div><img src='data:image/png;base64,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'></div>\n                    <div>\n                        <p>Kql Query Language, aka kql, is the query language for advanced analytics on Azure Monitor resources. The current supported data sources are \n                        Azure Data Explorer (Kusto), Log Analytics and Application Insights. To get more information execute '%kql --help \"kql\"'</p>\n                        <p>   \n                          &bull; \n                kql reference: Click on 'Help' tab > and Select 'kql reference' or execute '%kql --help \"kql\"'<br>\n                          &bull; \n                Kqlmagic configuration: execute '%config Kqlmagic'<br>\n                          &bull; \n                Kqlmagic usage: execute '%kql --usage'<br>\n                        </p> \n                    </div>\n                </div>\n            </body>\n            </html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<html>\n        <head>\n            \n            \n        </head>\n        <body>\n            <div><p style='padding: 10px; color: #3a87ad; background-color: #d9edf7; border-color: #bce9f1'>Kqlmagic&nbsp;package&nbsp;is&nbsp;updated&nbsp;frequently.&nbsp;Run&nbsp;&apos;!pip&nbsp;install&nbsp;Kqlmagic&nbsp;--no-cache-dir&nbsp;--upgrade&apos;&nbsp;to&nbsp;use&nbsp;the&nbsp;latest&nbsp;version.<br>Kqlmagic&nbsp;version:&nbsp;0.1.113.post1,&nbsp;source:&nbsp;https://github.com/Microsoft/jupyter-Kqlmagic</p></div>\n        </body>\n        </html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                }
            ],
            "execution_count": 3
        },
        {
            "cell_type": "markdown",
            "source": [
                "## Setup the connection"
            ],
            "metadata": {
                "azdata_cell_guid": "393052fc-020b-4eb6-96b6-feb166972d22"
            }
        },
        {
            "cell_type": "code",
            "source": [
                "%kql azureDataExplorer://code;cluster='help';database='Samples' -try-azcli_login"
            ],
            "metadata": {
                "azdata_cell_guid": "573614bc-73ae-4887-835e-06b63ecb01f1"
            },
            "outputs": [
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<!DOCTYPE html>\n            <html><body>\n            <div style=''>\n            <b>RH4PC5KSV</b>&nbsp;<a href='http://127.0.0.1:63485/webbrowser?url=http%3A//127.0.0.1%3A63485/files/.kqlmagic/temp_files/1e4b96d0-5990-4def-8af9-cf4cc59b9f27/popup_devicelogin.html%3Fkernelid%3D1e4b96d0-5990-4def-8af9-cf4cc59b9f27&kernelid=1e4b96d0-5990-4def-8af9-cf4cc59b9f27' style='padding: 2px 6px 2px 6px; color: #333333; background-color: #EEEEEE; border-top: 1px solid #CCCCCC; border-right: 1px solid #333333; border-bottom: 1px solid #333333; border-left: 1px solid #CCCCCC' target='popup_verification_url'>Copy code to clipboard and authenticate</a>\n            </div>\n            </body></html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<!DOCTYPE html>\n                            <html><body><script>\n\n                                // close authentication window\n                                if (kql_MagicUserCodeAuthWindow && kql_MagicUserCodeAuthWindow.opener != null && !kql_MagicUserCodeAuthWindow.closed) {\n                                    kql_MagicUserCodeAuthWindow.close()\n                                }\n                                // TODO: make sure, you clear the right cell. BTW, not sure it is a must to do any clearing\n\n                                // clear output cell\n                                Jupyter.notebook.clear_output(Jupyter.notebook.get_selected_index())\n\n                                // TODO: if in run all mode, move to last cell, otherwise move to next cell\n                                // move to next cell\n\n                            </script></body></html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<!DOCTYPE html>\n            <html><body>\n            <div style=''>\n            <a href='http://127.0.0.1:63485/webbrowser?url=http%3A//127.0.0.1%3A63485/files/.kqlmagic/temp_files/1e4b96d0-5990-4def-8af9-cf4cc59b9f27/popup__Samples_at_help_schema.html%3Fkernelid%3D1e4b96d0-5990-4def-8af9-cf4cc59b9f27&kernelid=1e4b96d0-5990-4def-8af9-cf4cc59b9f27' style='padding: 2px 6px 2px 6px; color: #333333; background-color: #EEEEEE; border-top: 1px solid #CCCCCC; border-right: 1px solid #333333; border-bottom: 1px solid #333333; border-left: 1px solid #CCCCCC' target='popup__Samples_at_help_schema'>popup schema Samples@help</a>\n            </div>\n            </body></html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                }
            ],
            "execution_count": 4
        },
        {
            "cell_type": "markdown",
            "source": [
                "## The query that would use the parameters"
            ],
            "metadata": {
                "azdata_cell_guid": "2362df1d-e14f-492a-a8d5-48e161c14a66"
            }
        },
        {
            "cell_type": "code",
            "source": [
                "%%kql \r\n",
                "let _state = stateFilter;\r\n",
                "StormEvents \r\n",
                "| where State == _state\r\n",
                "| summarize EventCount = count() by Event = EventType \r\n",
                "| order by EventCount desc\r\n",
                "| limit 10"
            ],
            "metadata": {
                "azdata_cell_guid": "a24b0ed9-7b4c-417f-87dd-753cbd80f3b2",
                "tags": []
            },
            "outputs": [
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<html>\n        <head>\n            \n            \n        </head>\n        <body>\n            <div><p style='padding: 10px; color: #3a87ad; background-color: #d9edf7; border-color: #bce9f1'>&nbsp;*&nbsp;Samples@help</p></div>\n        </body>\n        </html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "                 Event  EventCount\n0    Thunderstorm Wind         609\n1              Drought         533\n2                 Hail         269\n3         Frost/Freeze         122\n4            Lightning         106\n5       Excessive Heat         100\n6              Tornado          56\n7  Hurricane (Typhoon)          43\n8          Flash Flood          25\n9       Winter Weather          19",
                        "text/html": "<div>\n<style scoped>\n    .dataframe tbody tr th:only-of-type {\n        vertical-align: middle;\n    }\n\n    .dataframe tbody tr th {\n        vertical-align: top;\n    }\n\n    .dataframe thead th {\n        text-align: right;\n    }\n</style>\n<table border=\"1\" class=\"dataframe\">\n  <thead>\n    <tr style=\"text-align: right;\">\n      <th></th>\n      <th>Event</th>\n      <th>EventCount</th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <th>0</th>\n      <td>Thunderstorm Wind</td>\n      <td>609</td>\n    </tr>\n    <tr>\n      <th>1</th>\n      <td>Drought</td>\n      <td>533</td>\n    </tr>\n    <tr>\n      <th>2</th>\n      <td>Hail</td>\n      <td>269</td>\n    </tr>\n    <tr>\n      <th>3</th>\n      <td>Frost/Freeze</td>\n      <td>122</td>\n    </tr>\n    <tr>\n      <th>4</th>\n      <td>Lightning</td>\n      <td>106</td>\n    </tr>\n    <tr>\n      <th>5</th>\n      <td>Excessive Heat</td>\n      <td>100</td>\n    </tr>\n    <tr>\n      <th>6</th>\n      <td>Tornado</td>\n      <td>56</td>\n    </tr>\n    <tr>\n      <th>7</th>\n      <td>Hurricane (Typhoon)</td>\n      <td>43</td>\n    </tr>\n    <tr>\n      <th>8</th>\n      <td>Flash Flood</td>\n      <td>25</td>\n    </tr>\n    <tr>\n      <th>9</th>\n      <td>Winter Weather</td>\n      <td>19</td>\n    </tr>\n  </tbody>\n</table>\n</div>",
                        "application/vnd.dataresource+json": {
                            "schema": {
                                "fields": [
                                    {
                                        "name": "Event",
                                        "type": "string"
                                    },
                                    {
                                        "name": "EventCount",
                                        "type": "integer"
                                    }
                                ],
                                "kqmagic_version": "0.1.113.post1"
                            },
                            "data": [
                                {
                                    "Event": "Thunderstorm Wind",
                                    "EventCount": 609
                                },
                                {
                                    "Event": "Drought",
                                    "EventCount": 533
                                },
                                {
                                    "Event": "Hail",
                                    "EventCount": 269
                                },
                                {
                                    "Event": "Frost/Freeze",
                                    "EventCount": 122
                                },
                                {
                                    "Event": "Lightning",
                                    "EventCount": 106
                                },
                                {
                                    "Event": "Excessive Heat",
                                    "EventCount": 100
                                },
                                {
                                    "Event": "Tornado",
                                    "EventCount": 56
                                },
                                {
                                    "Event": "Hurricane (Typhoon)",
                                    "EventCount": 43
                                },
                                {
                                    "Event": "Flash Flood",
                                    "EventCount": 25
                                },
                                {
                                    "Event": "Winter Weather",
                                    "EventCount": 19
                                }
                            ]
                        }
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<html>\n        <head>\n            \n            \n        </head>\n        <body>\n            <div><p style='padding: 10px; color: #3a87ad; background-color: #d9edf7; border-color: #bce9f1'>Done&nbsp;(00:00.296):&nbsp;10&nbsp;records</p></div>\n        </body>\n        </html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                },
                {
                    "data": {
                        "text/plain": "[{'Event': 'Thunderstorm Wind', 'EventCount': 609},\n {'Event': 'Drought', 'EventCount': 533},\n {'Event': 'Hail', 'EventCount': 269},\n {'Event': 'Frost/Freeze', 'EventCount': 122},\n {'Event': 'Lightning', 'EventCount': 106},\n {'Event': 'Excessive Heat', 'EventCount': 100},\n {'Event': 'Tornado', 'EventCount': 56},\n {'Event': 'Hurricane (Typhoon)', 'EventCount': 43},\n {'Event': 'Flash Flood', 'EventCount': 25},\n {'Event': 'Winter Weather', 'EventCount': 19}]",
                        "text/html": ""
                    },
                    "metadata": {},
                    "execution_count": 10,
                    "output_type": "execute_result"
                }
            ],
            "execution_count": 10
        },
        {
            "cell_type": "code",
            "source": [
                "%%kql \n",
                "let _state = stateFilter;\n",
                "StormEvents \n",
                "| where State == _state\n",
                "| summarize event_count=count() by bin(StartTime, 1d) \\\n",
                "| render timechart title= 'Daily Storm Events'"
            ],
            "metadata": {
                "azdata_cell_guid": "570abf22-9214-4f39-a386-aad2026f277e"
            },
            "outputs": [
                {
                    "data": {
                        "text/plain": "<IPython.core.display.HTML object>",
                        "text/html": "<html>\n        <head>\n            \n            \n        </head>\n        <body>\n            <div><p style='padding: 10px; color: #b94a48; background-color: #f2dede; border-color: #eed3d7'>query&nbsp;execution&nbsp;error:<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;&quot;error&quot;:&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@ClientRequestLogger&quot;:&nbsp;&quot;&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@context&quot;:&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityId&quot;:&nbsp;&quot;0c4e7917-7be8-4125-939f-146f0f97df12&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityStack&quot;:&nbsp;&quot;(Activity&nbsp;stack:&nbsp;CRID=Kqlmagic.execute;6ade347c-f2ac-41a2-aa8b-1769ae8c98ff&nbsp;ARID=0c4e7917-7be8-4125-939f-146f0f97df12&nbsp;>&nbsp;KD.Query.Client.ExecuteQueryAsKustoDataStream/59e9cb51-092c-4e37-a33c-c1da9543c9b1&nbsp;>&nbsp;P.WCF.Service.ExecuteQueryInternalAsKustoDataStream..IClientServiceCommunicationContract/8d149ea4-febc-4191-8539-f5051d4e1cff&nbsp;>&nbsp;DN.FE.ExecuteQuery/d202f7f3-c744-47a8-8bc7-fcfcdb57c86d)&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityType&quot;:&nbsp;&quot;DN.FE.ExecuteQuery&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;appDomainName&quot;:&nbsp;&quot;Kusto.WinSvc.Svc.exe&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;clientRequestId&quot;:&nbsp;&quot;Kqlmagic.execute;6ade347c-f2ac-41a2-aa8b-1769ae8c98ff&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;machineName&quot;:&nbsp;&quot;KEngine000001&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;parentActivityId&quot;:&nbsp;&quot;8d149ea4-febc-4191-8539-f5051d4e1cff&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;processId&quot;:&nbsp;13028,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;processName&quot;:&nbsp;&quot;Kusto.WinSvc.Svc&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;serviceAlias&quot;:&nbsp;&quot;HELP&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;subActivityId&quot;:&nbsp;&quot;d202f7f3-c744-47a8-8bc7-fcfcdb57c86d&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;threadId&quot;:&nbsp;768,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;timestamp&quot;:&nbsp;&quot;2021-04-23T22:18:14.0489776Z&quot;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@database&quot;:&nbsp;&quot;Samples&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@message&quot;:&nbsp;&quot;Request&nbsp;is&nbsp;invalid&nbsp;and&nbsp;cannot&nbsp;be&nbsp;processed:&nbsp;Syntax&nbsp;error:&nbsp;SYN0001:&nbsp;I&nbsp;could&nbsp;not&nbsp;parse&nbsp;that,&nbsp;sorry.&nbsp;[line:position=0:0].&nbsp;Query:&nbsp;&apos;let&nbsp;stateFilter&nbsp;=&nbsp;&apos;GEORGIA&apos;;let&nbsp;_state&nbsp;=&nbsp;stateFilter;\\nStormEvents&nbsp;\\\\\\n|&nbsp;summarize&nbsp;event_count=count()&nbsp;by&nbsp;bin(StartTime,&nbsp;1d)&nbsp;\\\\\\n|&nbsp;where&nbsp;State&nbsp;==&nbsp;_state&nbsp;\\\\\\n|&nbsp;render&nbsp;timechart&nbsp;title=&nbsp;&apos;Daily&nbsp;Storm&nbsp;Events&apos;&apos;&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@permanent&quot;:&nbsp;true,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@text&quot;:&nbsp;&quot;let&nbsp;stateFilter&nbsp;=&nbsp;&apos;GEORGIA&apos;;let&nbsp;_state&nbsp;=&nbsp;stateFilter;\\nStormEvents&nbsp;\\\\\\n|&nbsp;summarize&nbsp;event_count=count()&nbsp;by&nbsp;bin(StartTime,&nbsp;1d)&nbsp;\\\\\\n|&nbsp;where&nbsp;State&nbsp;==&nbsp;_state&nbsp;\\\\\\n|&nbsp;render&nbsp;timechart&nbsp;title=&nbsp;&apos;Daily&nbsp;Storm&nbsp;Events&apos;&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@type&quot;:&nbsp;&quot;Kusto.Data.Exceptions.KustoBadRequestException&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;code&quot;:&nbsp;&quot;General_BadRequest&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;innererror&quot;:&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@context&quot;:&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityId&quot;:&nbsp;&quot;0c4e7917-7be8-4125-939f-146f0f97df12&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityStack&quot;:&nbsp;&quot;(Activity&nbsp;stack:&nbsp;CRID=Kqlmagic.execute;6ade347c-f2ac-41a2-aa8b-1769ae8c98ff&nbsp;ARID=0c4e7917-7be8-4125-939f-146f0f97df12&nbsp;>&nbsp;KD.Query.Client.ExecuteQueryAsKustoDataStream/59e9cb51-092c-4e37-a33c-c1da9543c9b1&nbsp;>&nbsp;P.WCF.Service.ExecuteQueryInternalAsKustoDataStream..IClientServiceCommunicationContract/8d149ea4-febc-4191-8539-f5051d4e1cff&nbsp;>&nbsp;DN.FE.ExecuteQuery/d202f7f3-c744-47a8-8bc7-fcfcdb57c86d)&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;activityType&quot;:&nbsp;&quot;DN.FE.ExecuteQuery&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;appDomainName&quot;:&nbsp;&quot;Kusto.WinSvc.Svc.exe&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;clientRequestId&quot;:&nbsp;&quot;Kqlmagic.execute;6ade347c-f2ac-41a2-aa8b-1769ae8c98ff&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;machineName&quot;:&nbsp;&quot;KEngine000001&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;parentActivityId&quot;:&nbsp;&quot;8d149ea4-febc-4191-8539-f5051d4e1cff&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;processId&quot;:&nbsp;13028,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;processName&quot;:&nbsp;&quot;Kusto.WinSvc.Svc&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;serviceAlias&quot;:&nbsp;&quot;HELP&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;subActivityId&quot;:&nbsp;&quot;d202f7f3-c744-47a8-8bc7-fcfcdb57c86d&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;threadId&quot;:&nbsp;768,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;timestamp&quot;:&nbsp;&quot;2021-04-23T22:18:14.0489776Z&quot;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@errorCode&quot;:&nbsp;&quot;SYN0001&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@errorMessage&quot;:&nbsp;&quot;I&nbsp;could&nbsp;not&nbsp;parse&nbsp;that,&nbsp;sorry.&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@line&quot;:&nbsp;&quot;0&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@message&quot;:&nbsp;&quot;Syntax&nbsp;error:&nbsp;SYN0001:&nbsp;I&nbsp;could&nbsp;not&nbsp;parse&nbsp;that,&nbsp;sorry.&nbsp;[line:position=0:0].&nbsp;Query:&nbsp;&apos;let&nbsp;stateFilter&nbsp;=&nbsp;&apos;GEORGIA&apos;;let&nbsp;_state&nbsp;=&nbsp;stateFilter;\\nStormEvents&nbsp;\\\\\\n|&nbsp;summarize&nbsp;event_count=count()&nbsp;by&nbsp;bin(StartTime,&nbsp;1d)&nbsp;\\\\\\n|&nbsp;where&nbsp;State&nbsp;==&nbsp;_state&nbsp;\\\\\\n|&nbsp;render&nbsp;timechart&nbsp;title=&nbsp;&apos;Daily&nbsp;Storm&nbsp;Events&apos;&apos;&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@permanent&quot;:&nbsp;true,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@pos&quot;:&nbsp;&quot;0&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;@type&quot;:&nbsp;&quot;Kusto.Data.Exceptions.SyntaxException&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;code&quot;:&nbsp;&quot;SYN0001&quot;,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;message&quot;:&nbsp;&quot;I&nbsp;could&nbsp;not&nbsp;parse&nbsp;that,&nbsp;sorry.&quot;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;message&quot;:&nbsp;&quot;Request&nbsp;is&nbsp;invalid&nbsp;and&nbsp;cannot&nbsp;be&nbsp;executed.&quot;<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</p></div>\n        </body>\n        </html>"
                    },
                    "metadata": {},
                    "output_type": "display_data"
                }
            ],
            "execution_count": 14
        },
        {
            "cell_type": "code",
            "source": [
                ""
            ],
            "metadata": {
                "azdata_cell_guid": "69e6a490-26bb-453f-a16f-c994428c888b"
            },
            "outputs": [],
            "execution_count": null
        }
    ]
}